# Dhanhar Masala — Application Screen Reference

## Overview

This document is a screen-by-screen reference for the Dhanhar Masala trading/ERP application. It captures the purpose, fields, buttons, and table columns of each screen as currently built, and is intended as a working reference during planning and development of the v1 rebuild.

**In scope:** every screen reachable from the main navigation — authentication, dashboard, purchase, sales, accounting, and inventory.
**Out of scope:** backend logic, API contracts, and database schema (tracked separately).
**Maintainers:** update this file whenever a screen's fields or layout change; treat it as part of the release checklist, not an afterthought.

## Table of Contents

- [Authentication](#authentication)
  - [Login Page](#login-page)
  - [Select Company Page](#select-company-page)
- [Dashboard](#dashboard)
  - [Dashboard](#dashboard-1)
  - [Daily Diary](#daily-diary)
  - [Voucher Details (popup)](#voucher-details-popup)
  - [Outstanding](#outstanding)
  - [Pin Board](#pin-board)
  - [Analysis (Quality Analysis)](#analysis-quality-analysis)
  - [Visit Planning](#visit-planning)
  - [Party Visit Plan List](#party-visit-plan-list)
  - [Party Detail](#party-detail)
  - [Party Zoom (Buyer Zoom)](#party-zoom-buyer-zoom)
  - [Party Order History (popup)](#party-order-history-popup)
  - [Price Matrix](#price-matrix)
- [Purchase](#purchase)
  - [Journal Purchase](#journal-purchase)
  - [Journal Purchase Report](#journal-purchase-report)
  - [Purchase Invoice (Tax Invoice)](#purchase-invoice-tax-invoice)
  - [Purchase Invoice Report](#purchase-invoice-report)
  - [Purchase Return](#purchase-return)
  - [Purchase Return Report](#purchase-return-report)
  - [Purchase Register](#purchase-register)
  - [Purchase Return Register](#purchase-return-register)
  - [Purchase Matrix](#purchase-matrix)
  - [Purchase Brokerage Report](#purchase-brokerage-report)
  - [Majuri Report (Purchase Majuri)](#majuri-report-purchase-majuri)
  - [Purchase Report (Purchase Quality Report)](#purchase-report-purchase-quality-report)
- [Sales](#sales)
  - [Journal Sales](#journal-sales)
  - [Journal Sales Report](#journal-sales-report)
  - [Sales Invoice (Tax Invoice)](#sales-invoice-tax-invoice)
  - [Sales Invoice Report](#sales-invoice-report)
  - [E-Invoice Print](#e-invoice-print)
  - [Sales Return](#sales-return)
  - [Sales Return Report](#sales-return-report)
  - [Sales Register](#sales-register)
  - [SalesMan Report](#salesman-report)
  - [Sales Report (Sales Quality Report)](#sales-report-sales-quality-report)
- [Accounting](#accounting)
  - [Voucher (Receipt / Payment / Contra / Journal)](#voucher-receipt--payment--contra--journal)
  - [Receipt Voucher Multi](#receipt-voucher-multi)
  - [Voucher Report (Receipt / Payment / Contra / Journal)](#voucher-report-receipt--payment--contra--journal)
  - [Settlement](#settlement)
  - [Ledger](#ledger)
  - [Matrix Outstanding](#matrix-outstanding)
  - [Matrix](#matrix)
  - [Cash (Cash Statement)](#cash-cash-statement)
  - [Cash Register](#cash-register)
  - [Bank (Cheque Deposit)](#bank-cheque-deposit)
  - [Bank Register](#bank-register)
  - [Bank Reco Auto (Bank Reconciliation)](#bank-reco-auto-bank-reconciliation)
  - [Interest Ledger](#interest-ledger)
  - [Multi JV (Journal Voucher Entries)](#multi-jv-journal-voucher-entries)
- [Inventory](#inventory)
  - [Stock Detail](#stock-detail)
  - [Stock Matrix](#stock-matrix)
  - [Stock Journal](#stock-journal)
  - [Stock Report](#stock-report)
  - [Stock Journal Report](#stock-journal-report)
  - [Stock Transfer](#stock-transfer)
  - [Stock Transfer Report](#stock-transfer-report)
  - [Godown Wise Stock](#godown-wise-stock)
- [Glossary](#glossary)

Each screen entry follows the same structure — **Purpose**, **Navigation** (where known), **Fields**, **Buttons**, **Table columns**, and **Bottom rows** where applicable — so entries are easy to scan and compare.

---

## Authentication

### Login Page

**Purpose:** Entry point to the system. Authenticates users and takes them to the Dashboard.

**Fields:**

- **App Code** — text input. Likely a company/tenant identifier (this platform is used by multiple client companies, so App Code tells it which company's data to load). For our build, we probably don't need this — flag for review.
- **Username** — text input
- **Password** — text input, masked

**Buttons:**

- **Login** — submits the form, validates credentials, redirects to Dashboard
- **Scan QR to log in with an app** — alternate login via mobile app QR scan. Skip for v1.
- **Register Face** — face-recognition based login. Skip for v1.

### Select Company Page

**Purpose:** Appears right after login. Lets the user pick which Financial Year, Company, and Branch they want to work in, before landing on the Dashboard.

**Fields** (all dropdowns, in this order, each likely filtering the next):

- **Financial Year** — e.g. "2023-2024". Probably lists all years data exists for.
- **Company** — e.g. "DHANHAR PRODUCTS LLP 2023-2024". Likely filtered by the selected Financial Year.
- **Branch** — e.g. "BHAGAL RETAIL BRANCH". Likely filtered by selected Company. Note: "Retail Branch" suggests there may be multiple branch *types* — worth watching for e.g. a "Wholesale Branch" too on other screens.

**Buttons:**

- **Go** — confirms the selection, takes the user into the Dashboard scoped to that Year + Company + Branch
- **Log out** — top right, exits back to Login page

---

## Dashboard

### Dashboard

**Purpose:** Main landing page after selecting company/branch. Shows an overview of the business: buyers, orders, money, GST (Goods and Services Tax) data, sales/purchase trend, and party analysis.

**Fields:**

- Search box (top, "Party…")
- Show entries dropdown — on Party Analysis table
- Search box — inside Party Analysis table

**Buttons:**

- Today — on Money widget
- Purchase / Sales — on trend chart
- Bank Data — on GST Data widget
- Party Analysis
- Gear/settings icon
- Print, Excel — on Party Analysis table
- Column sort arrows — on all Party Analysis columns

### Daily Diary

**Purpose:** Date-wise summary of orders, sales, purchases, deliveries, and return cheques.

**Fields:**

- Date range — from date, to date

**Buttons:**

- GO
- Heart icon — next to heading
- Gear/settings icon
- Person icon — on each card, opens Voucher Details popup

**Table columns (Return Cheque List):**

- Party Name, Cheque Date, Cheque Reference No, Amount, Deposit Date, Return Date

### Voucher Details (popup)

**Purpose:** Opens from the person icon on a Daily Diary card; shows the vouchers behind that card's number.

**Fields:** None

**Buttons:**

- X — close

**Table columns:**

- SR, Voucher, Date, Voucher Type, Mode, Party Account, Amount, Remark

### Outstanding

**Purpose:** Shows party-wise outstanding balance broken into aging buckets.

**Fields:**

- Select Type — dropdown
- Broker — dropdown
- Date range — from date, to date
- Bucket range input (0-30, 30-90…) — near the export icons
- Show entries dropdown
- Search — inside the table

**Buttons:**

- Go
- Heart icon — next to heading
- Envelope icon
- Gear/settings icon
- Print, Excel, Print icons — export row above table
- PDF icon, Excel icon — green icons above table
- Print, PDF, Excel — links next to table search
- Column sort arrows — on every column
- Row-level icons (PDF, Print, Excel, Envelope, another icon) — per party row on the right side

**Table columns:**

- #, Name, 0-30, 30-90, 90-180, 180-365, 366+, Balance, and a last column with the row-level icons

### Pin Board

**Purpose:** A sticky-note style board for jotting down quick notes/reminders.

**Fields:** None visible yet (likely appears after clicking + to add a note)

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- "+" icon — on the sticky note, likely to add a new note

### Analysis (Quality Analysis)

**Purpose:** Shows item-wise sales/stock performance over a date range — how much of each product was sold, stock movement, and active party count.

**Fields:**

- From date, To date
- Search — inside table

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Purchase — button top right (likely switches this analysis to Purchase side instead of Sales)
- Submit
- Print, PDF, Excel
- Column sort arrows — on every column

**Table columns:**

- SR, Quality Name, Sold, Material Sold, Material %, Party, Active Party, Party %, Stock In, Stock Out, Stock Sold %

### Visit Planning

**Purpose:** Shows planned/missed party visits, day-wise, with future visits also listed.

**Fields:**

- Search
- Date picker

**Buttons:**

- Heart icon — next to heading
- Today's Plan
- Visit List
- Gear/settings icon
- Date navigation arrows — next to the date heading (e.g. 11-09-2026)
- Action dropdown — on each visit card under the date column

**Data shown:**

- Missed Order column — party cards with two dates and a number badge
- Date column (e.g. 11-09-2026) — party cards with a date, two number badges (one green, one blue "Normal"), and Action dropdown
- Future column — empty in this view

### Party Visit Plan List

**Purpose:** Opens from Today's Plan / Visit List; shows visit plan entries in table form.

**Fields:**

- Show entries dropdown
- Search
- Date picker

**Buttons:**

- Heart icon
- Gear/settings icon
- Visit Planning — button top right
- Previous, Next, page number — pagination
- Rupee icon, pencil/edit icon — per row on the right

**Table columns:**

- SR, Name, Visit Type, Purpose, Assigned/Call To, Mobile No, Status

### Party Detail

**Purpose:** Opens on clicking a record. Shows full detail for a party: contact info, quick action buttons, sales summary, and ledger.

**Fields:**

- Search box (top, e.g. shows "sund" — party name search)
- Date range — from date, to date (for Ledger section)

**Buttons:**

- Gear/settings icon
- Receipt, Payment, Invoice, Return, Order, Ledger, Outstanding, Quality, Sales Qty — action buttons
- GO — next to Ledger date range
- Print, file/document, Excel, Envelope, WhatsApp icons — next to party name in Ledger table

**Data shown (left panel):**

- Party name, Pay Day, address, contact person name, mobile number, email, GST number (two codes shown), sales amount, amount due, credit limit %, return goods amount, a small trend chart (line graph, months on x-axis)

**Table columns (Ledger, right panel):**

- Date, LFNO, Particular, Remark, Ref Detail, Ref No, Debit, Credit, Balance
- Closing Balance row and Total row at the bottom

### Party Zoom (Buyer Zoom)

**Purpose:** Visual box/tile view of parties (buyer/supplier/broker/quality), color-coded, each box clickable to show order history.

**Fields:** None visible

**Buttons:**

- Heart icon — next to heading
- Buyer, Supplier, Broker, Quality — tabs
- Print icon, Excel icon, Gear/settings icon
- Move/arrows icon (below the tab row)
- Party boxes (e.g. Shailesh Trading Co, Cash Sales Bhagal, R K Traders, Jai Durga Trading) — clickable, opens popup

**Data shown:**

- Colored tiles, one per party, sized differently, each showing party name

### Party Order History (popup)

**Purpose:** Opens on clicking a party tile in Party Zoom; shows that party's order-wise history.

**Fields:** None

**Buttons:**

- X — close

**Table columns:**

- Order No., Date, Diff, (unlabeled column with a number badge), Amount, Diff, (unlabeled column with a highlighted amount badge)

### Price Matrix

**Purpose:** Shows quality-wise price/quantity breakdown, branch-wise, with a unit selector.

**Fields:**

- Unit dropdown (search box inside it) — options: KGS, PCS
- Search — inside table

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Branch tabs — Bhagal Branch, Bhagal Retail Branch, Devjinagar Retail Branch, Ichhapore Branch, Katargam Main Branch, Katargam Retail Branch
- Column sort arrows — on every column

**Table columns:**

- Quality Name, N/A, 0.008, 0.01, 0.012, 0.016, 0.02, 0.025, 0.04, 0.05, 0.1, 0.2, 0.5, 1, 5, 20

---

## Purchase

### Journal Purchase

**Purpose:** Form to record a purchase transaction, with line items for goods and tax breakdown.

**Fields:**

- Invoice No.
- Invoice Date
- Supplier — dropdown, with a "+" icon next to it
- Remark
- TDS (Tax Deducted at Source) Applicable — checkbox
- Search — inside the item table, at the bottom
- Add — link below search

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Calendar icon — next to Invoice Date
- "+" icon — next to Supplier
- TCS (Tax Collected at Source) [%] input, TCS button
- Round Off input
- Add — below the table

**Table columns:**

- Name, HSN (Harmonized System of Nomenclature code), GST, Unit, Qty, Rate Per, Rate, Amount, Disc Per, Disc, Taxable, SGST, CGST, IGST, Total

**Bottom rows:** Final Total row, TCS [%] input row, Round Off row

### Journal Purchase Report

**Purpose:** Lists all journal purchase entries with filters, totals, and row-level actions.

**Fields:**

- Date range — from date, to date
- Show entries dropdown
- Column filter inputs — Date, Invoice No, Supplier, Taxable, Amount, Remark (under each header)

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Go
- Export/print icons — row of colored icons above the table (multiple, different export formats)
- Column sort arrows — on every column
- Row-level action icons — pencil/edit, trash/delete, X (orange), print, question mark/info, upload, download — per row
- Previous, page numbers (1-6), Next — pagination

**Table columns:**

- Date, Invoice No, Supplier, Taxable, SGST, CGST, IGST, Amount, Remark, Action

**Bottom rows:**

- Page subtotal row (100 entries shown, with column totals)
- Grand Total row (Amount: 0.00)

### Purchase Invoice (Tax Invoice)

**Purpose:** Form to create a purchase invoice with quality-wise line items, godown selection, and tax breakdown.

**Fields:**

- Invoice Type — radio buttons: Tax Invoice, Bill of Supply, Invoice
- Account — dropdown
- Supplier — radio + dropdown, with "+" icon
- Receiving Goods Address — radio + dropdown
- Invoice No.
- Invoice Date
- Godown — dropdown
- Cash Payment — checkbox
- Remark
- Search — inside item table, bottom
- Add — link below search

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Calendar icon — next to Invoice Date
- "+" icon — next to Supplier
- Add Quality — button, above table
- TCS input, Shipping input, Round Off input — bottom right of table
- Add — below search

**Table columns:**

- SR, Quality Name, Qty Per, Unit Sent, Pkg, Qty Sent, Rate Per, Rate, Total, Disc(%), Disc(Rs), Freight, SGST, CGST, IGST, Amount

**Bottom row:** Final Total row

### Purchase Invoice Report

**Purpose:** Lists purchase invoices with filters, totals, and export options.

**Fields:**

- Select — dropdown (×2)
- Date range — from date, to date
- All — dropdown, next to export icons
- Show entries dropdown
- Column filter inputs — Invoice No, Challan No, Supplier, Unit, Quantity, Taxable, Tax (under headers)

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- New Due, Due — top right
- Go
- Export icons — print, Excel, PDF, envelope, print, another export icon (row above table)
- Column sort arrows — on every column
- Previous, Next — pagination

**Table columns:**

- Date, Invoice No, Challan No, Type, Supplier, Unit, Quantity, Taxable, SGST, CGST, IGST, Tax, Amount, TCS, Action

**Bottom rows:**

- Supplier subtotal row
- Grand Total row — Unit, Quantity, Netmeter, Amount, Taxable, SGST, CGST, IGST, Tax, TCS

### Purchase Return

**Purpose:** Form to record a purchase return, credit note, or debit note against a supplier invoice.

**Fields:**

- Return Type — radio buttons: Purchase Return, Credit Note, Debit Note
- Account — dropdown
- Prefix
- Credit Note No.
- Date
- Supplier — radio + dropdown
- Broker — dropdown
- Haste — radio + dropdown
- Receiving Goods Address — radio + dropdown
- Invoice No. — dropdown (Select Some Options)
- Godown — dropdown
- Transporter — dropdown
- Other Transporter
- LR (Lorry Receipt) No.
- Bale Marka
- Remark
- Search — inside item table, bottom

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Calendar icon — next to Date
- TCS [%] input, TCS toggle/button
- Round Off input

**Table columns:**

- SR, Quality Name, HSN, GST, Unit, Qty Per, Quantity, Unit Sent, Quantity Sent, Rate Per, Rate, Amount, Disc(%), Disc(Rs), Taxable Value, SGST, CGST, IGST, Total Amount

**Bottom rows:** Round Off row, Final Total row

### Purchase Return Report

**Purpose:** Lists purchase return/credit note/debit note entries with filters and totals.

**Fields:**

- Return Type — radio buttons: Purchase Return, Purchase Credit Note, Purchase Debit Note
- Date range — from date, to date
- Show entries dropdown
- Search — inside table

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Go
- Export icons — print, Excel, PDF, envelope, print, another export icon (row above table)
- Print icon — second row, standalone
- Column sort arrows — on every column
- Previous, Next — pagination

**Table columns:**

- Credit Note No, Date, Supplier, Invoice No, Unit, Quantity, Total Taxable, Total, Action

**Bottom rows:**

- Subtotal row
- Grand Total row — Unit, Quantity, Netmeter, Taxable Amount, Amount

### Purchase Register

**Purpose:** Month-wise summary of purchases with tax breakdown, plus a bar chart visualization.

**Fields:**

- All, Select, All Branch, All Head, ALL — dropdowns
- Date range — from date, to date

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Export icons — print, PDF, Excel, envelope (row above table)
- Print icon, Excel icon — per row, right side
- Scroll-to-top arrow — bottom left

**Table columns:**

- #, Month, Taxable, CGST, SGST, IGST, Tax, Amount, Total, Action

**Data shown (below table):** Bar chart — monthly totals, April through March on x-axis

### Purchase Return Register

**Purpose:** Month-wise summary of purchase returns with a bar chart visualization.

**Fields:**

- Select — dropdown
- Date range — from date, to date

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Go
- Export icons — print, Excel (row above table)

**Table columns:**

- #, Month, Taxable, Tax, Amount, Total

**Bottom row:** Total row

**Data shown (below table):** Bar chart — monthly totals, April through March on x-axis

### Purchase Matrix

**Purpose:** Shows quality-wise purchase quantity/amount breakdown by unit size, with a unit selector.

**Fields:**

- Unit dropdown (search box inside it) — options: KGS, PCS
- Search — top right, partially visible

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Column sort arrows — on every column

**Table columns:**

- Quality Name, N/A, 0.008, 0.01, 0.012, 0.016, 0.02, 0.025, 0.04, 0.05, 0.1, 0.2, 0.5, 1, 5, 20, Total

### Purchase Brokerage Report

**Purpose:** Shows brokerage-wise purchase transactions with received/pending amounts.

**Fields:**

- Broker/Party dropdown (search box inside it) — options include Bagreeji Smart Products LLP, R K Masala, Sunfab Designer Shirting, and several other named/phone-number entries
- Date range — from date, to date
- Show entries dropdown
- Search — inside table

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- GO
- Print icon
- Column sort arrows — on every column
- Previous, Next — pagination

**Table columns:**

- Date, Invoice, Buyer, Unit, Quantity, Amount, Rec/Ret, Pending

### Majuri Report (Purchase Majuri)

**Purpose:** Shows majuri (labor charge) figures grouped under Sales, Purchase, Sales Return, and Purchase Return sections.

**Fields:**

- Date range — from date, to date

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- GO
- Print icon
- Scroll-to-top arrow — bottom left

**Sections shown (each currently empty, no data/table visible):** Sales, Purchase, Sales Return, Purchase Return

### Purchase Report (Purchase Quality Report)

**Purpose:** Lists purchase transactions quality-wise with tax breakdown.

**Fields:**

- Select, All, All — dropdowns
- ALL — dropdown (top right)
- Date range — from date, to date
- Show entries dropdown
- Column filter inputs — Date, Invoice No, Supplier Name, Quality Name, Qty, Rate, CGST, SGST, IGST, Taxable Value, Invoice Value, Transporter Name (under headers)
- Search — inside table

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- GO
- Export icons — print, Excel, PDF, envelope (row above table)
- Print — link next to table search
- Column sort arrows — on every column
- Previous, page numbers (1-6), Next — pagination
- Scroll-to-top arrow — bottom left

**Table columns:**

- Date, Invoice No, Supplier Name, Quality Name, Qty, Rate, CGST, SGST, IGST, Taxable Value, Invoice Value, Transporter Name

**Bottom rows:**

- Page subtotal row (Qty, CGST, SGST, IGST, Taxable Value, Invoice Value totals)
- Grand Total row — Taka, TCS Amount, Invoice Value

---

## Sales

### Journal Sales

**Purpose:** Form to record a sales transaction, with line items for goods and tax breakdown.

**Fields:**

- Prefix
- Invoice No.
- LF (Ledger Folio) No.
- Invoice Date
- Buyer — dropdown, with "+" icon next to it
- Credit Days
- Remark
- Search — inside item table, bottom

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Calendar icon — next to Invoice Date
- "+" icon — next to Buyer
- Round Off input

**Table columns:**

- Name, HSN, GST, Unit, Qty, Rate Per, Rate, Amount, Disc, Taxable, SGST, CGST, IGST, Total

**Bottom rows:** Round Off row, Final Total row

### Journal Sales Report

**Purpose:** Lists all journal sales entries with filters, totals, and row-level actions.

**Fields:**

- Select — dropdown
- Date range — from date, to date
- Show entries dropdown
- Search — inside table

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Go
- Export icons — print, Excel, PDF, print, another export icon (row above table)
- Column sort arrows — on every column
- Previous, Next — pagination

**Table columns:**

- Date, Invoice No, Buyer, SGST, CGST, IGST, Amount, Action

**Bottom rows:**

- Subtotal row
- Grand Total row (Amount: 0.00)

### Sales Invoice (Tax Invoice)

**Purpose:** Form to create a sales invoice with quality-wise line items, delivery details, and tax breakdown.

**Fields:**

- Challan Type — radio buttons: Tax Invoice, Bill of Supply, Invoice
- Account — dropdown
- Buyer — radio + dropdown, with "+" icon
- Haste — radio + dropdown
- Delivery Party Godown — radio + dropdown
- Delivery Days
- Remark
- Invoice No.
- Invoice Date
- Godown — dropdown
- Transporter — dropdown, with "+" icon
- Other Transporter
- Vehicle No.
- Transport Paid — checkbox
- Cash Payment — checkbox
- Search — top right, above item table
- Search — inside item table, bottom
- Add — link below search

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Calendar icon — next to Invoice Date
- "+" icon — next to Buyer, next to Transporter
- Cash Receive input
- Cash Back field (display)

**Table columns:**

- SR, Quality Name, GST, Unit Sent, Pkg, Qty Sent, Rate, Help, Total, Disc(%), Disc(Rs), Freight, Taxable, SGST, CGST, Total

**Bottom rows:** Round Off row, Final Total row

### Sales Invoice Report

**Purpose:** Lists sales invoices with filters, totals, and export options.

**Fields:**

- Select — dropdown (×2)
- Date range — from date, to date
- All — dropdown, next to export icons
- Show entries dropdown
- Column filter inputs — Invoice No, Date, Buyer, Quantity, Taxable, CGST, SGST, IGST, Amount (under headers)

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Due, New Due — top right
- Print icon — top right, standalone
- Go
- Export icons — multiple colored icons (row above table)
- Column sort arrows — on every column
- Previous, Next — pagination

**Table columns:**

- Invoice No, Date, Buyer, GSTN, Quantity, Taxable, CGST, SGST, IGST, Amount, Action

**Bottom rows:**

- Subtotal row
- Total row — Total Rolls, Total Meter, Total Netmeter, Total Amount

### E-Invoice Print

**Purpose:** Lists sales invoices with e-invoice (IRN/ACK) related fields for e-invoice generation/printing.

**Fields:**

- Select — dropdown (×2)
- Date range — from date, to date
- All — dropdown, next to export icons
- Show entries dropdown
- Column filter inputs — Invoice No, Transporter, Date, Buyer, Amount (under headers)

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Due — top right
- Go
- Export icons — multiple colored icons (row above table)
- Column sort arrows — on every column
- Previous, Next — pagination

**Table columns:**

- Invoice No, Transporter, Date, Buyer, GSTN, Amount, ACK No, ACK Date, Distance, Action

**Bottom rows:**

- Subtotal row
- Total row — Total Rolls, Total Meter, Total Netmeter, Total Amount

### Sales Return

**Purpose:** Form to record a sales return, credit note, or debit note against a buyer invoice.

**Fields:**

- Return Type — radio buttons: Sales Return, Credit Note, Debit Note
- Account — dropdown
- Prefix
- Credit Note No.
- Date
- Buyer — radio + dropdown
- Haste — radio + dropdown
- Broker — dropdown
- Delivery Party Godown — radio + dropdown
- Invoice No. — dropdown (Select Some Options)
- Godown — dropdown
- Transporter — dropdown
- Other Transporter
- LR No.
- Remark
- Without Inventory — checkbox
- Cash Payment — checkbox
- Document No.
- Document Date
- Search — inside item table, bottom

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Calendar icon — next to Date, next to Document Date

**Table columns:**

- SR, Quality Name, HSN, GST, Unit, Qty Per, Qty, Unit Received, Quantity Received, Rate Per, Rate, Amount, Disc(%), Disc(Rs), Taxable Value, SGST, CGST, IGST, Total Amount

**Bottom rows:** Round Off row, Final Total row

### Sales Return Report

**Purpose:** Lists sales return/credit note/debit note entries with filters and totals.

**Fields:**

- Return Type — radio buttons: Sales Return, Sales Credit Note, Sales Debit Note
- ALL — dropdown
- Date range — from date, to date
- Show entries dropdown
- Search — inside table

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Go
- Export icons — multiple colored icons (row above table)
- Column sort arrows — on every column
- Previous, Next — pagination

**Table columns:**

- No, Date, Buyer, Quality Name, Haste, Broker, Invoice No, Unit, Quantity, Total Taxable, Total, ACKNO, ACKDate, Quality Remark, Action

**Bottom rows:**

- Subtotal row
- Total row — Total Unit, Total Quantity, Total Netmeter, Total Taxable Amount, Total Amount

### Sales Register

**Purpose:** Month-wise summary of sales with tax breakdown, plus a bar chart visualization.

**Fields:**

- All, Select Account, Select, All Branch — dropdowns
- Date range — from date, to date

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- Go
- Export icons — print, PDF, envelope (row above table)
- Print icon — per row, right side
- Scroll-to-top arrow — bottom left

**Table columns:**

- #, Month, Taxable, CGST, SGST, IGST, Tax, Amount, Total, Action

**Data shown (below table):** Bar chart — monthly totals, April through March on x-axis

### SalesMan Report

**Purpose:** Shows salesman-wise sales transactions with received/pending amounts.

**Fields:**

- Select — dropdown
- Date range — from date, to date

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- GO
- Export icons — print, PDF, Excel, envelope (row above table)
- Column filter inputs — under each header

**Table columns:**

- Date, Invoice, Buyer, Unit, Quantity, Amount, Rec/Ret, Pending

### Sales Report (Sales Quality Report)

**Purpose:** Lists sales transactions quality-wise with tax breakdown.

**Fields:**

- Select, All, Select, All — dropdowns
- Date range — from date, to date
- Show entries dropdown
- Column filter inputs — Date, Invoice No, Buyer Name, GSTN, Quality Name, Qty, Kg, Kg, Rate, Discount %, Discount Rs., Taxable Value (under headers)

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon
- GO
- Export icons — multiple colored icons, two rows (print, Excel, PDF, envelope, print, more)
- Print — link next to table
- Column sort arrows — on every column
- Previous, page numbers, Next — pagination
- Scroll-to-top arrow — bottom left

**Table columns:**

- Date, Invoice No, Buyer Name, GSTN, Quality Name, Quality Type, Qty, Kg, Kg, Rate, Discount %, Discount Rs., Taxable Value, CGST, SGST (more columns likely continue beyond visible area)

**Bottom rows:**

- Page subtotal row (Qty, Kg, Kg, Discount Rs., Taxable Value totals)
- Grand Total row — Taka, Meter, Kg, Discount Rs., Taxable Value, Invoice Value

---

## Accounting

### Voucher (Receipt / Payment / Contra / Journal)

**Purpose:** Single form to record accounting vouchers, with tabs switching between Receipt, Payment, Contra, and Journal types. A TDS section appears when applicable.

**Fields (Receipt tab):**

- Voucher No., Voucher Date
- Transaction Type — dropdown (e.g. Net Banking)
- Party Account — dropdown, with "+" icon
- Bank Account — dropdown (shows balance, e.g. "7717701.59 DR")
- Ref No., Ref Date, Amount, Remark
- TDS Applicable — checkbox

**Fields (Payment tab):**

- Voucher No., Voucher Date — with calendar picker
- Transaction Type — dropdown (e.g. Net Banking)
- Party Account — dropdown, with "+" icon
- Bank Account — dropdown (shows balance)
- Chq/NEFT Ref No., Chq/NEFT Date, Amount, Remark
- TDS Applicable — checkbox
- (When TDS checked) Amount Per TDS, TDS Account, Nature Of Payment, Status, Applicable Rate, TDS

**Fields (Contra tab):**

- Voucher No., LF No., Voucher Date
- Voucher Type — dropdown (e.g. Cash Deposit)
- From Account — dropdown, with "+" icon (shows balance)
- To Account — dropdown
- Amount, Remark
- Print — checkbox

**Fields (Journal tab):**

- Voucher No., LF No., Voucher Date
- Transaction Type — dropdown (e.g. Journal Voucher)
- Debit Party Account — radio + dropdown, with "+" icon
- Credit Party Account — radio + dropdown
- Amount, Remark
- TDS Applicable — checkbox
- (When TDS checked) TDS Account, Nature Of Payment, Status, Applicable Rate, TDS

**Buttons (common across all tabs):**

- Heart icon, Gear/settings icon
- Multi Payment Voucher / Multi Journal Voucher — top right (tab-specific label)
- Calendar icon — next to date fields
- "+" icon — next to account dropdowns

### Receipt Voucher Multi

**Purpose:** Bulk entry screen for recording multiple receipt/payment/journal vouchers at once.

**Fields:**

- Voucher Type — tabs: Receipt, Payment, Journal
- Enter No., Voucher Date
- Transaction Type — dropdown
- Show TDS Section — checkbox
- Cash Account — dropdown
- Total Amount

**Buttons:**

- Heart icon, Gear/settings icon
- Go, Submit

**Table columns:**

Two grouped sections — **Voucher**: #, Voucher No, LF No, Party, Amount, Remarks; **Tran Detail**: Ref No, Ref Date.

When "Show TDS Section" is checked, a third group appears — **TDS Detail**: TDS Applicable, Amount Per TDS, TDS Account, Nature Of Payment, Status, Applicable Rate, TDS.

### Voucher Report (Receipt / Payment / Contra / Journal)

**Purpose:** Lists recorded vouchers, tab-switchable by voucher type, with filters, totals, and row-level actions.

**Fields (Receipt tab):**

- Select PartyBroker
- Select — dropdown (Report Print / Report View / VoucherPrint InvoiceSet)
- Date range — from date, to date
- Show entries dropdown, Search
- Column filter inputs — VoucherNo, VoucherDate, VoucherType, TxnType, Bank, Party, City, ChequeNo, Amount, Remark

**Fields (Payment tab):** Same as Receipt, with Select dropdown options Select / Cash / Bank / Net Banking.

**Fields (Contra tab):**

- Date range, Show entries dropdown, Search
- Column filter inputs — VoucherNo, VoucherDate, VoucherType, DebitParty, CreditParty, Amount, Remark

**Fields (Journal tab):**

- Date range, Show entries dropdown, Search
- Column filter inputs — VoucherNo, VoucherDate, VoucherType, DebitParty_Name, CreditParty_Name, Amount, Remark

**Buttons (common across all tabs):**

- Heart/list icon, Gear/settings icon
- Print, PDF, Excel icons — top right
- Report Print / Default — dropdowns, top right
- Go
- CSV, Excel, PDF, Print — links next to search
- Column sort arrows — on every column
- Row-level action icons — expand, delete, X, print, info, upload, download, envelope, another icon (varies slightly per tab)
- Previous, Next — pagination (Receipt/Payment tabs)

**Table columns (Receipt/Payment tabs):** VoucherNo, VoucherDate, VoucherType, TxnType, Bank, Party, City, ChequeNo, Amount, Remark, Action

**Table columns (Contra tab):** VoucherNo, VoucherDate, VoucherType, DebitParty, CreditParty, Amount, Remark, Action

**Table columns (Journal tab):** VoucherNo, VoucherDate, VoucherType, DebitParty_Name, CreditParty_Name, Amount, Remark, Action

**Bottom row (Receipt/Payment tabs):** Amount total row

### Settlement

**Purpose:** Lets a party's transactions (invoices, receipts, payments) be settled against each other, split into Settled and Un Settled sections.

**Fields:**

- Party dropdown (search box inside it) — options include Bagreeji Smart Products LLP, Cash Bhagal, R K Masala, Sunfab Designer Shirting, and several other named parties

**Buttons:**

- Heart icon, Gear/settings icon
- Print icon, Submit
- Three number values shown top right (likely summary figures; labels not visible)

**Sections shown:** Settled (left, empty in this view), Un Settled (right, empty in this view)

### Ledger

**Purpose:** Shows a party's full transaction ledger — debit/credit entries with running balance.

**Fields:**

- Party — dropdown
- Date range — from date, to date
- Show entries dropdown, Search

**Buttons:**

- Gear/settings icon
- Export icons — print, Excel, PDF, print, envelope
- GO
- Column sort arrows — on every column
- Previous, page number, Next — pagination

**Table columns:**

- SR, Date, LFNO, Particular, Remark, Ref Detail, Ref No, Debit, Credit, Balance

**Rows shown:** Opening Balance row, Closing Balance row, Total row (Debit, Credit, Balance)

### Matrix Outstanding

**Purpose:** Summary view showing outstanding totals split into Debtors (Sales side) and Creditors (Purchase side).

**Fields:** None visible

**Buttons:** Heart icon, Gear/settings icon

**Table 1 columns (Debtors):** Name, Grand Total — Rows: Sales, Receive, Current Month, Old Month, Debtors

**Table 2 columns (Creditors):** Name, Grand Total — Rows: Purchase, Payment, Current Month, Old Month, Creditors

### Matrix

**Purpose:** Shows a broker-wise breakdown for a selected transaction type (Receipt Voucher, Payment Voucher, Sales, Sales Return, Sales Journal, Purchase, Purchase Return, Purchase Journal, Direct Indirect).

**Fields:**

- Type dropdown (search box inside it) — options: Direct Indirect, Receipt Voucher, Payment Voucher, Sales, Sales Return, Sales Journal, Purchase, Purchase Return, Purchase Journal
- Show entries dropdown, Search

**Buttons:**

- Heart icon, Gear/settings icon
- Go
- Excel, PDF, Print — links next to search
- Column sort arrows — on every column
- Previous, Next — pagination

**Table columns:** SR, Name, Broker, Grand Total

**Bottom row:** Total row

### Cash (Cash Statement)

**Purpose:** Shows day-wise cash transactions with running balance.

**Fields:**

- Account dropdown (e.g. Cash)
- Date range — from date, to date
- Show entries dropdown, Search

**Buttons:**

- Heart icon, Gear/settings icon
- GO
- Column sort arrows — on every column

**Table columns:** SR, Voucher Date, Particulars, Voucher Type, Voucher No, Transaction Type, Debit, Credit, Balance

**Rows shown:** Opening Balance row

### Cash Register

**Purpose:** Month-wise cash summary with running balance, plus a bar chart visualization.

**Fields:** Account dropdown (e.g. Cash)

**Buttons:**

- Heart icon, Gear/settings icon
- Export icons — print, PDF, Excel (top right)
- Print icon — per row, right side

**Table columns:** #, Month, Debit, Credit, Amount, Action

**Rows shown:** Opening Balance row

**Data shown (below table):** Bar chart — monthly totals, April through March on x-axis

### Bank (Cheque Deposit)

**Purpose:** Drag-and-drop interface to move cheques between Cleared and Return status.

**Fields:** Date picker

**Buttons:** Heart icon, Gear/settings icon, GO

**Sections shown (drag-and-drop zones):**

- Cleared Cheque List — with date shown per zone
- Cheque Return List — with date shown per zone

### Bank Register

**Purpose:** Month-wise bank account summary with running balance, plus a bar chart visualization.

**Fields:** Account dropdown (search box inside it) — options: Axis Bank, Bank Of Baroda, HDFC Bank, KMBL

**Buttons:**

- Heart icon, Gear/settings icon
- Print icon — top right, and per row

**Table columns:** #, Month, Debit, Credit, Amount, Action

**Rows shown:** Opening Balance row

**Data shown (below table):** Bar chart — monthly totals (positive and negative values), April through March on x-axis

### Bank Reco Auto (Bank Reconciliation)

**Purpose:** Reconciles bank transactions against system-recorded vouchers, using an uploaded bank statement file, across three related tables.

**Fields:**

- Party/Broker dropdown
- Choose file — file upload input (bank statement)

**Buttons:**

- Heart icon, Gear/settings icon
- Auto Reco
- Expand/fullscreen icon — top right of table area

**Table 1 columns:** SR, Date, Voucher Type, Transaction Type, Chq/Ref, Deposited Date, Debit, Credit, Old Reco, New Reco, Bank Remark

**Table 2 columns:** SR, Date, Particulars, Chq/Ref, Debit, Credit

**Table 3 columns:** SR, Date, Voucher Type, Transaction Type, Chq/Ref, Deposited Date, Debit, Credit

### Interest Ledger

**Purpose:** Calculates interest on a party's outstanding balance based on debit/credit rate percentages over a date range.

**Fields:**

- Select Party — dropdown
- Start Date, End Date
- Dr %, Cr %
- Enter Days, Gp Dr, Gp Cr

**Buttons:** Heart icon, Gear/settings icon, GO, Print, Excel

**Table columns:** Name, Balance

**Rows shown:** Total, Interest, Total With Interest

### Multi JV (Journal Voucher Entries)

**Purpose:** Bulk entry screen for multi-line journal vouchers with debit/credit type selection.

**Fields:**

- Voucher number input
- Select — dropdown
- Dr/Cr dropdown (search box inside it) — options: Dr, Cr
- Voucher Date
- Show entries dropdown, Search
- Name — dropdown, per row (shown as "SELECT")
- Amount — input, per row

**Buttons:** Heart icon, Gear/settings icon, Go, Submit, Previous/page number/Next — pagination

**Table columns:** SR, Name, Amount

---

## Inventory

### Stock Detail

**Purpose:** Shows quality-wise stock movement (opening, bought, sold, closing) per godown, with a godown filter.

**Fields:**

- Date range — from date, to date
- Godown tabs — All, Bhagal Godown, Ichhapore, Jainam Trade Link LLP, Surat Agro Cold Storage, Uma Akash Agro Pvt.Ltd, Bhagal Retail Godown, Devjinagar Godown, Icchapore P/C, Katargam, Katargam Retail Godown
- Show entries dropdown, Search

**Buttons:**

- Heart icon, Gear/settings icon
- GO
- Export icons — multiple colored icons (row above table)
- Column sort arrows — on every column
- Previous, page numbers, Next — pagination

**Table columns:** #, Quality Name, Opening, Bought, Sold, Closing (each cell shows two stacked values — likely unit and quantity)

**Bottom row:** Total Unit, Total Quantity

### Stock Matrix

**Purpose:** Shows quality-wise stock quantity breakdown by unit size, per branch-godown combination, with a unit selector.

**Fields:**

- Unit dropdown (search box inside it) — options: KGS, PCS
- Branch-Godown tabs — All, Bhagal Branch-Bhagal Godown, Bhagal Branch-Ichhapore, Bhagal Branch-Jainam Trade Link LLP, Bhagal Branch-Uma Akash Agro Pvt.Ltd (more tabs likely continue beyond visible area)
- Search — inside table

**Buttons:**

- Heart icon, Gear/settings icon
- Column sort arrows — on every column
- Scroll-to-top arrow — bottom left

**Table columns:** Quality Name, N/A, 0.008, 0.01, 0.012, 0.016, 0.02, 0.025, 0.04, 0.05, 0.1, 0.2, 0.5, 1, 5, 20, Total

**Bottom row:** Column totals row

### Stock Journal

**Purpose:** Form to record a manual stock adjustment/journal entry, converting between sale and purchase quantities per quality.

**Fields:**

- Voucher No., Voucher Date
- Godown — dropdown
- Remark
- Search — top right, and inside item table

**Buttons:** Heart icon, Gear/settings icon, Calendar icon — next to Voucher Date

**Display-only fields:**

- Difference (shows a ratio, e.g. "0 / 0.000")
- Voucher Type (shows "Stock Journal Voucher")

**Table columns:** SR, Quality Name, Sale Unit, Sale Qty, Sales Per, Purchase Unit, Purchase Qty, Sales Per

**Bottom row:** Total row

### Stock Report

**Purpose:** Shows a stock movement summary with three views — All (line-item breakdown), Grey MonthWise, and Finish MonthWise — tracking stock across shop, mill, and reprocessing stages.

**Fields:**

- Branch — dropdown (e.g. Bhagal Branch)
- Date range — from date, to date
- View toggle — radio buttons: All, Grey MonthWise, Finish MonthWise

**Buttons:**

- Heart icon, Gear/settings icon
- Go
- Export icons — multiple colored icons (row above table)
- Row-level export icon (Action column) — per line, All view only

**Table columns (All view):** Description, #, StockQty, Value, Action — Rows: Opening Grey, Grey Purchase, Grey Purchase Return, Grey Sales, Grey Sales Return, Grey Send To Mill, Grey Return From Mill, Grey Stock At Shop, Opening At Mill, Grey Send To Mill, Received From Mill, Re-Process To Mill, Received From Re-Process, Grey Return From Mill, Shortage At Mill, Elongated (Excess MTS)

**Table columns (Grey MonthWise view, table 1):** Month, (+) Open Grey, (+) Grey Pur., (-) Grey Pur.Return, (-) Grey Sales, (+) Grey Sales.Return, (-) Send To Mill, (+) Rtn From Mill, (+) Grey From Mill, (=) Grey At Shop

**Table columns (Grey MonthWise view, table 2):** Month, (+) Open At Mill, (+) Grey Send To Mill, (+) Refinish, (-) Rec. From Mill, (-) Grey Return From Mill, (-) Grey Receive From Mill, (-) Rec. From Refinish, (-) Loss At Mill, (+) Elongated, (=) Stock At Mill

**Table columns (Finish MonthWise view):** Month, (+) OpenFinished, (+) FinishPur, (-) FinishPurr, (+) RecdFrmMill, (-) Refinished, (+) ReceiveRefinished, (-) Sales, (+) SalesRtn, (+) Elongated, (=) FinStock

**Bottom row:** Total row (MonthWise views)

### Stock Journal Report

**Purpose:** Lists stock journal entries (quality-wise stock movement records) with sorting, search, and pagination. Currently showing no data.

**Navigation:** Home / Accounting / Stock Journal Report (accessed via Inventory → Stock Journal Report in sidebar)

**Fields:**

- Branch — shown in top bar (e.g. Bhagal Branch), not a page-level filter here
- Show entries — dropdown (e.g. 100) controlling rows per page
- Search — text box, searches across table

**Buttons:**

- Gear/settings icon — top right
- Print icon (orange) — top right
- Sort arrows — on each sortable column header
- Previous / Next — pagination controls

**Table columns:** No, Date, Quality Name, Unit, Qty, Per, Type, Remark, Action

### Stock Transfer

**Purpose:** Create/manage a stock transfer between godowns — includes transfer details header and a line-item table for quality-wise transfer.

**Navigation:** Home / Inventory / Stock Transfer

**Fields:**

- Transfer No. — text/auto-filled (e.g. 1256)
- Transfer Date — date picker
- From Godown — dropdown
- To Godown — dropdown
- Transporter — text
- LR No. — text
- LF No. — text
- Driver Name — text
- Driver Mob No. — text
- Vehicle No. — text
- Employee — text
- Expense — text
- Remark — textarea
- Search — text box (above table, filters table)
- Search — text box (below table, secondary filter)

**Buttons:** Heart icon — next to heading; Gear/settings icon — top right

**Table columns:** SR, Quality Name, Units Sent, Quantity Sent, Rate Per

**Bottom row:** Total row

### Stock Transfer Report

**Purpose:** Lists all stock transfer transactions between godowns with quality, quantity, and remark details — sortable, searchable, paginated.

**Navigation:** Home / Inventory / Stock Transfer Report

**Fields:**

- Show entries — dropdown (e.g. 100) controlling rows per page
- Search — text box, searches across table

**Buttons:**

- Heart icon — next to heading
- Gear/settings icon, Print icon (orange), Print icon (green), Export icon (green) — top right
- Sort arrows — on Date, Issue For, Quantity columns
- No (transfer no.) — clickable link per row, opens that transfer

**Table columns:** No, Date, Quality, Issue For, From, To, Unit, Quantity, LFNO, Remark

### Godown Wise Stock

**Purpose:** Shows material-wise opening, purchase, sell, and closing stock (unit, qty, rate, amount) for each godown, with a separate table block per godown.

**Navigation:** Home / Inventory / Godown Wise Stock

**Fields:** No visible filters on this view (godown blocks are shown sequentially for all godowns, e.g. Bhagal Godown, Surat Agro Cold Storage, Uma Akash Agro Pvt.Ltd, Ichhapore)

**Buttons:** Heart icon; Print icon, Excel export icon, PDF export icon, Gear/settings icon — top right

**Table columns (per godown block):** Material, Opening (Unit, Qty, Rate, Amount), Purchase (Unit, Qty), Sell (Unit, Qty), Closing (Unit, Qty, Rate, Amount)

**Rows:** Hing, Masala, Chilly Powder, Haldi Powder, Dhana Powder, Rajgara Lot, Shingoda Lot, Rock Salt, Amchur Powder, Jira Powder Loose, Mari Powder, Variyali, Rai, Oil, Chilly Powder-PCS, Dry Fruit 5%, Sabudana, Rajgara (list varies slightly per godown)

**Bottom row:** Total row (per godown block)

**Structure:** Multiple godown blocks stacked vertically, each with its own header bar (godown name) and full table.

---

## Glossary

| Term | Meaning |
|---|---|
| GST | Goods and Services Tax |
| SGST / CGST / IGST | State / Central / Integrated GST |
| TDS | Tax Deducted at Source |
| TCS | Tax Collected at Source |
| HSN | Harmonized System of Nomenclature (product classification code) |
| LF No. | Ledger Folio number |
| LR No. | Lorry Receipt number |
| SR | Serial number (row number) |
| GSTN | GST identification Number |
| ACK No. / ACK Date | Acknowledgement number/date for e-invoice (IRN) filing |
| Godown | Warehouse/storage location |
| Haste | Transport/dispatch term used for delivery hand-off party |
| Majuri | Labor/handling charge |
