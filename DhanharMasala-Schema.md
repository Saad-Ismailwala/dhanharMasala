# Dhanhar Masala — Database Schema Design

Derived from `DhanharMasala.md` (UI/screen inventory). This doc filters that inventory down to
**what needs to become a table/column** vs **what is UI-only noise** (icons, export buttons,
pagination, search boxes) vs **what should be a computed report, not a stored table**.

Same section order as the source doc, so you can cross-reference screen → table easily.

---

## Schema Conventions

- Every transaction table gets: `id`, `branch_id`, `financial_year_id`, `created_at`, `created_by`,
  `updated_at`, `updated_by` — not repeated per table below, assume it.
- Every header table with line items follows `xxx_header` + `xxx_line` split (1-to-many).
- `account` is the **single unified ledger master** — Buyer, Supplier, Broker, Bank, Cash, Expense,
  Asset are all rows in `account` differentiated by `account_type`. The source doc's "Party
  Balance," "Buyer," "Supplier," "Broker" dropdowns are all pulling from this one table — don't
  build four separate master tables, you'll break reconciliation and ledger views.
- Icons (Heart, Gear, Print, PDF, Excel, Envelope, sort arrows, pagination, "Show entries",
  in-table Search) → **UI-only, not schema.** Skipped everywhere below without re-noting it.
- Fields marked `SKIP (v1)` are real but deferrable — noted so nothing gets silently lost.
- Fields marked `→ derived` are report-only outputs (computed at query time), not stored columns.

---

## 0. Core Masters

These are referenced by almost every transaction table below — build these first.

**`company`**
| column | type | notes |
|---|---|---|
| id | PK | |
| name | varchar | |
| gstin | varchar | company-level, branches may override |

**`branch`**
| column | type | notes |
|---|---|---|
| id | PK | |
| company_id | FK → company | |
| name | varchar | e.g. "Bhagal Branch", "Katargam Retail Branch" |
| gstin | varchar | branch-specific GSTIN (seen in GST Summary, GSTR1/2/3B — each branch files separately) |
| address, city, state, state_code | | state_code needed for State Wise GST Report |

**`financial_year`**
| column | type | notes |
|---|---|---|
| id | PK | |
| start_date, end_date | date | every report/register screen filters by this — make it first-class, not just a date-range widget |

**`user`**
| column | type | notes |
|---|---|---|
| id | PK | |
| username, password_hash | | |
| role | enum | permission scoping — the doc doesn't show role-based UI differences explicitly, but multi-branch + multi-company access implies this is needed |
| face_id_data | — | **SKIP (v1)** — Register Face login noted as skip in source |
| qr_login_token | — | **SKIP (v1)** — QR login noted as skip in source |

**`godown`**
| column | type | notes |
|---|---|---|
| id | PK | |
| branch_id | FK | godowns are branch-scoped per Stock Detail's godown tabs |
| name | varchar | e.g. Bhagal Godown, Ichhapore, Jainam Trade Link LLP |

**`unit`**
| column | type | notes |
|---|---|---|
| id | PK | |
| name | varchar | KGS, PCS |
| pack_size | decimal | the 0.008 / 0.01 / 0.012 ... 20 values in Price/Purchase/Stock Matrix are pack-size variants of a unit, not separate units — model as a `unit_pack_size` child table or a decimal column on the line item, not a new unit row per size |

**`quality`** (item master — "Quality Name" everywhere)
| column | type | notes |
|---|---|---|
| id | PK | |
| name | varchar | e.g. Hing, Masala, Chilly Powder, Haldi Powder |
| hsn_code | varchar | used in Purchase/Sales Invoice line items and GSTR1 HSN section |
| default_gst_rate | decimal | |
| default_unit_id | FK → unit | |
| stage | enum(grey/finish) | **only if** you're modeling the mill/reprocessing flow from Stock Report — otherwise skip; most quality items don't go through mill |

**`account`** (unified ledger master: Buyer/Supplier/Broker/Bank/Cash/Expense/Asset)
| column | type | notes |
|---|---|---|
| id | PK | |
| name | varchar | |
| account_type | enum | Buyer, Supplier, Broker, Bank, Cash, Expense, Asset, Transporter |
| group | varchar | "Group" column seen in Party Balance |
| gstin | varchar | Party Detail shows two GST codes — may need `account_gstin` child table if multi-GSTIN per account is real, confirm before deciding |
| address, city, state, area, area_code, contact_person, mobile, email | | from Party Detail + Party Balance |
| registration_date | date | |
| opening_balance, opening_dr_cr | decimal, enum | |
| credit_limit_pct, credit_days, pay_day | | from Party Detail panel |
| bank_name, bank_account_no, ifsc | — | **only for account_type = Bank** |
| commission_rate | decimal | **only for account_type = Broker** — needed for Brokerage Sales Report calculations |

**`transporter`**
| column | type | notes |
|---|---|---|
| id | PK | |
| name, contact | | could fold into `account` as account_type=Transporter instead — pick one, don't duplicate |

**`tds_section`** (master, from TDS Rate screen)
| column | type | notes |
|---|---|---|
| id | PK | |
| old_section, new_section, code | varchar | |
| nature_of_payment | varchar | |
| rate_individual, rate_others | decimal | |
| threshold, threshold_aggregate, threshold_type | | |
| effective_fy | varchar | doc shows FY 2025-26 (legacy) vs FY 2026-27 onwards toggle — version this by FY, don't overwrite |

**`depreciation_asset_category`**
| column | type | notes |
|---|---|---|
| id | PK | |
| name | varchar | Furniture, Computer Assets, Motor Car, etc. |
| applicable_rate | decimal | editable per source doc |

---

## 1. Authentication & System Scope

**Not a schema concern** — Login/Select Company are auth flow against `user`, `company`,
`branch`, `financial_year` above. No new tables.

---

## 2. Dashboard

Mostly **→ derived** (aggregation queries over transaction tables below). Two exceptions need real tables:

**`pin_board_note`**
| column | type | notes |
|---|---|---|
| id, branch_id, user_id | | |
| content | text | |
| created_at | | |

**`party_visit_plan`**
| column | type | notes |
|---|---|---|
| id | PK | |
| account_id | FK → account | the party being visited |
| visit_type, purpose | varchar | |
| assigned_to | FK → user | "Assigned/Call To" |
| planned_date | date | |
| status | enum | Pending/Done/Missed — drives the Visit Planning "Missed/Date/Future" columns |

Everything else in Dashboard (Money widget, Party Analysis, Outstanding aging buckets, Party Zoom
tiles, Price Matrix) is a **query over Sales/Purchase/Voucher tables**, not its own table. Don't
build a `party_analysis` table — it'll drift out of sync with the source data.

---

## 3. Purchase

**`purchase_journal_header`** + **`purchase_journal_line`**
- header: invoice_no, invoice_date, supplier_id (→account), remark, tds_applicable, round_off
- line: quality_id, hsn, gst_rate, unit_id, qty, rate_per, rate, amount, disc_pct, disc_amt, taxable, sgst, cgst, igst, total

**`purchase_invoice_header`** + **`purchase_invoice_line`**
- header: invoice_type (Tax Invoice/Bill of Supply/Invoice), account_id, supplier_id, delivery_address_id, invoice_no, invoice_date, godown_id, cash_payment, remark, tcs, shipping, round_off
- line: sr, quality_id, qty_per, unit_sent_id, pkg, qty_sent, rate_per, rate, total, disc_pct, disc_amt, freight, sgst, cgst, igst, amount

**`purchase_return_header`** + **`purchase_return_line`**
- header: return_type (Purchase Return/Credit Note/Debit Note), account_id, prefix, credit_note_no, date, supplier_id, broker_id, haste, delivery_address_id, against_invoice_id (FK → purchase_invoice_header), godown_id, transporter_id, other_transporter, lr_no, bale_marka, remark, tcs, round_off
- line: same shape as purchase_invoice_line, plus `qty_received`, `unit_received_id`

**Reports (3.2, 3.4, 3.6, 3.7–3.12) → all derived**, no new tables. Purchase Register/Return
Register month-wise bar charts, Purchase Matrix, Brokerage Report, Majuri Report, Purchase Quality
Report — all are `GROUP BY` queries over `purchase_invoice_line` / `purchase_return_line`.

**One real gap**: Majuri (labor charge) isn't captured as a field anywhere in the Purchase Invoice
form in the source doc — if it needs to be calculated, either add a `majuri_rate` column to
`purchase_invoice_line`/`sales_invoice_line`, or it's currently manual/external. Flag this for the
person who owns majuri logic before finalizing.

---

## 4. Sales

Mirrors Purchase exactly — same header/line pattern, buyer instead of supplier.

**`sales_journal_header`** + **`sales_journal_line`**
- header: prefix, invoice_no, lf_no, invoice_date, buyer_id (→account), credit_days, remark, round_off
- line: same shape as purchase_journal_line

**`sales_invoice_header`** + **`sales_invoice_line`**
- header: challan_type, account_id, buyer_id, haste, delivery_godown_id, delivery_days, remark, invoice_no, invoice_date, godown_id, transporter_id, other_transporter, vehicle_no, transport_paid, cash_payment, cash_receive, cash_back, round_off
- line: sr, quality_id, gst_rate, unit_sent_id, pkg, qty_sent, rate, total, disc_pct, disc_amt, freight, taxable, sgst, cgst, total
- **e-invoice fields** (separate child table `sales_invoice_einvoice`, 1-to-1, not on every row): irn, ack_no, ack_date, distance — only Sales Invoice needs this, don't pollute the base table

**`sales_return_header`** + **`sales_return_line`**
- header: return_type, account_id, prefix, credit_note_no, date, buyer_id, haste, broker_id, delivery_godown_id, against_invoice_id, godown_id, transporter_id, other_transporter, lr_no, remark, without_inventory (bool), cash_payment, document_no, document_date, round_off
- line: mirrors purchase_return_line

**Reports (4.2, 4.4, 4.5, 4.7–4.10) → all derived.** SalesMan Report needs a `salesman_id` FK
somewhere — the source doc doesn't show a Salesman field on the Sales Invoice form itself, so
either it's missing from the UI capture or it's derived from broker/user context. Confirm before
building — don't invent a `salesman` table speculatively.

---

## 5. Accounting

This is the module where getting the schema wrong is most expensive — get `voucher` right first.

**`voucher`** (unifies Receipt/Payment/Contra/Journal — one table, `voucher_type` enum)
| column | type | notes |
|---|---|---|
| id | PK | |
| voucher_type | enum | Receipt, Payment, Contra, Journal |
| voucher_no, lf_no, voucher_date | | |
| transaction_type | varchar | e.g. "Net Banking" |
| debit_account_id, credit_account_id | FK → account | **both nullable, populate based on type**: Receipt sets credit_account=party, debit_account=bank; Payment is reverse; Contra uses from/to; Journal uses debit/credit party directly. Don't build 4 separate voucher tables — Voucher Report screen already treats them as one filterable set. |
| ref_no, ref_date | | Chq/NEFT ref |
| amount, remark | | |
| tds_applicable | bool | |

**`voucher_tds_detail`** (1-to-1 with voucher, only when tds_applicable)
| column | type |
|---|---|
| voucher_id | FK |
| amount_per_tds, tds_account_id, nature_of_payment, status, applicable_rate, tds_amount | |

**Receipt Voucher Multi / Multi JV (5.2, 5.14)** — these are bulk-entry UI patterns, not a new
schema. They insert multiple rows into `voucher` in one submit. No separate table needed.

**`settlement_allocation`** (junction table — this is the piece most likely to be missed)
| column | type | notes |
|---|---|---|
| id | PK | |
| account_id | FK → account | |
| voucher_id | FK → voucher, nullable | |
| invoice_id | FK, nullable | polymorphic-ish: points to sales_invoice_header or purchase_invoice_header — consider a `invoice_type` discriminator column instead of true polymorphism |
| settled_amount | decimal | |
| status | enum(settled/unsettled) | matches the Settlement screen's two sections |

**`bank_reconciliation_entry`**
| column | type | notes |
|---|---|---|
| id | PK | |
| account_id | FK → account (bank) | |
| voucher_id | FK → voucher, nullable | matched system-side entry |
| bank_statement_date, chq_ref, debit, credit | | from uploaded bank statement file |
| reco_status | enum(old_reco/new_reco/unmatched) | |
| bank_remark | varchar | |

**`interest_ledger_config`** (per party interest calculation params — 5.13/7.7 are the same screen)
| column | type |
|---|---|
| account_id | FK |
| dr_rate_pct, cr_rate_pct, grace_days, grace_dr, grace_cr | |

Interest **result** itself (Total, Interest, Total With Interest) → **derived**, computed at query
time from `voucher` + date range + this config. Don't store computed interest.

**Ledger, Matrix Outstanding, Matrix, Cash, Cash Register, Bank Register (5.5–5.11) → all
derived** views over `voucher` + `account`. No new tables.

---

## 6. Inventory

**`stock_journal_header`** + **`stock_journal_line`**
- header: voucher_no, voucher_date, godown_id, remark
- line: quality_id, sale_unit_id, sale_qty, sales_per, purchase_unit_id, purchase_qty

**`stock_transfer_header`** + **`stock_transfer_line`**
- header: transfer_no, transfer_date, from_godown_id, to_godown_id, transporter (free text or FK — source shows free text field, inconsistent with `transporter` master used elsewhere; recommend converting to FK for consistency), lr_no, lf_no, driver_name, driver_mobile, vehicle_no, employee, expense, remark
- line: quality_id, unit_sent_id, qty_sent, rate_per

**Stock Detail / Stock Matrix / Stock Report / Godown Wise Stock (6.1, 6.2, 6.4, 6.8) → all
derived.** Opening/Bought/Sold/Closing per quality per godown is a running computation over
`purchase_invoice_line` + `purchase_return_line` + `sales_invoice_line` + `sales_return_line` +
`stock_transfer_line` + `stock_journal_line`, not a stored table. Storing it invites drift.
**Exception**: if query performance at scale (thousands of qualities × godowns × months) makes
live computation too slow, add a `stock_snapshot` materialized/rollup table keyed by
(quality_id, godown_id, period) — but treat that as a performance optimization added later, not
part of the core schema.

---

## 7. Reports

Every screen in this section (7.1–7.11) is a **grouped/filtered view over tables already defined
above** — Order Sales/Purchase Report needs one new concept:

**`sales_order`** / **`purchase_order`** (the source doc's Reports section implies orders exist
upstream of invoices — "Order No", "Status: Pending/Ordered/Completed" — but no Order entry screen
appears anywhere in sections 3 or 4. This is a **gap in the source capture**, not something to
guess a schema for. Go back and find/screenshot the actual Order entry screen before modeling
`sales_order_header`/`line` — don't invent fields for a form you haven't seen.)

Party Balance (7.9), TCS/TDS Party (7.10), TCS Matrix (7.11), Rate Send (7.8) → all derived from
`account` + transaction tables, except:

**`rate_send_log`**
| column | type |
|---|---|
| id, account_id, sent_at, rate_file_ref | |

---

## 8. Tax

Almost everything here is **regulatory reporting, not storage** — GST Summary, GSTR1, GSTR2,
GSTR3B, State Wise GST Report, GST State Wise Summary are all computed from the tax fields already
sitting on `purchase_invoice_line` / `sales_invoice_line` / return lines. Do **not** create
`gstr1_table`, `gstr3b_table` etc. as stored data — you'll end up maintaining two sources of truth
for the same tax numbers.

The two exceptions that need real tables:

**`gst_filing_lock`** (once a period is filed, lock it so invoices can't silently change the
already-filed numbers)
| column | type |
|---|---|
| branch_id, period_month, period_year, gstr_type, filed_at, locked | |

**`itc04_challan`** + **`itc04_challan_line`** (job-work goods movement — genuinely transactional, not derivable from Sales/Purchase since job-work challans aren't regular invoices)
- header: direction (Mfg_to_JW / JW_to_Mfg), jobworker_account_id, challan_no, challan_date, branch_id
- line: quality_id, goods_type, description, uqc, qty, taxable_value, igst_rate, cgst_rate, sgst_rate, cess

**GSTR2 Reco (8.4)** needs one table since it's reconciling *external* data against yours:

**`gstr2a_import`** + **`gstr2a_import_line`** — raw uploaded 2A JSON, kept separate from your own
`purchase_invoice_line`, with a `reco_status` + `matched_purchase_invoice_line_id` for the
Match & Review screen.

**Depreciation Rate (8.13)**: `depreciation_asset_category` (already defined in §0) covers the
master. The actual asset instances (with book amount, purchase date) need a proper fixed-asset
register table if this isn't already tracked elsewhere — the source doc only shows category-level
rates, not individual assets, so this may be a genuine gap to raise with whoever owns fixed assets.

---

## 9. Explicitly deferred / not schema-worthy

| Item | Why |
|---|---|
| Face-recognition login | Marked skip-for-v1 in source |
| QR-code login | Marked skip-for-v1 in source |
| Heart icon (favorite), Gear icon (settings) | Pure UI state, could be a generic `user_favorite_screen` table if you want favoriting to persist per-user — otherwise skip entirely |
| Export/Print/PDF/Excel/Envelope actions | Rendering concern, not schema |
| "Search", "Show entries", pagination, column sort | Frontend/query concern, not schema |

---

## 10. Summary — entity relationship at a glance

```
company ─< branch ─< financial_year (scoping, not FK chain exactly, but every txn carries branch_id + fy_id)

account (unified: buyer/supplier/broker/bank/cash/asset/transporter)
   ├─< purchase_invoice_header ─< purchase_invoice_line >─ quality, godown, unit
   ├─< purchase_return_header  ─< purchase_return_line
   ├─< purchase_journal_header ─< purchase_journal_line
   ├─< sales_invoice_header    ─< sales_invoice_line
   ├─< sales_return_header     ─< sales_return_line
   ├─< sales_journal_header    ─< sales_journal_line
   ├─< voucher (receipt/payment/contra/journal) ─< voucher_tds_detail
   ├─< settlement_allocation >─ voucher / invoice
   ├─< bank_reconciliation_entry
   ├─< party_visit_plan
   └─< interest_ledger_config

quality ─< purchase/sales line items, stock_journal_line, stock_transfer_line, itc04_challan_line
godown  ─< stock_transfer_header (from/to), stock_journal_header, invoice headers

gst_filing_lock — cuts across sales/purchase once a period is filed
gstr2a_import — external data, reconciled against purchase_invoice_line
```

**Build order recommendation**: `company → branch → financial_year → account → quality/unit →
godown` first (everything else FKs into these), then Purchase + Sales header/line tables (near
duplicates of each other, build together), then `voucher` + `settlement_allocation` (the trickiest
relational piece), then Inventory, then Tax exceptions last since most of Tax is reporting, not
storage.

**Before finalizing**: two real gaps surfaced above need answers from whoever owns the business
logic, not guesses — (1) where Sales/Purchase Orders actually get created (referenced in Reports
but no entry screen was captured), and (2) how Majuri (labor charge) is calculated and where it's
entered.
