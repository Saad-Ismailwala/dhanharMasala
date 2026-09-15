# Dhanhar Masala Application Documentation

## Table of Contents

- [Core Principles & Scope](#core-principles--scope)
- [1. Authentication & System Scope](#1-authentication--system-scope)
  - [1.1 Login Page](#11-login-page)
  - [1.2 Select Company Page](#12-select-company-page)
- [2. Dashboard](#2-dashboard)
  - [2.1 Dashboard](#21-dashboard)
  - [2.2 Daily Diary](#22-daily-diary)
  - [2.3 Voucher Details (popup)](#23-voucher-details-popup)
  - [2.4 Outstanding](#24-outstanding)
  - [2.5 Pin Board](#25-pin-board)
  - [2.6 Analysis (Quality Analysis)](#26-analysis-quality-analysis)
  - [2.7 Visit Planning](#27-visit-planning)
  - [2.8 Party Visit Plan List](#28-party-visit-plan-list)
  - [2.9 Party Detail (opens on clicking a record)](#29-party-detail-opens-on-clicking-a-record)
  - [2.10 Party Zoom (Buyer Zoom)](#210-party-zoom-buyer-zoom)
  - [2.11 Party Order History (popup)](#211-party-order-history-popup)
  - [2.12 Price Matrix](#212-price-matrix)
- [3. Purchase](#3-purchase)
  - [3.1 Journal Purchase](#31-journal-purchase)
  - [3.2 Journal Purchase Report](#32-journal-purchase-report)
  - [3.3 Purchase Invoice (Tax Invoice)](#33-purchase-invoice-tax-invoice)
  - [3.4 Purchase Invoice Report](#34-purchase-invoice-report)
  - [3.5 Purchase Return](#35-purchase-return)
  - [3.6 Purchase Return Report](#36-purchase-return-report)
  - [3.7 Purchase Register](#37-purchase-register)
  - [3.8 Purchase Return Register](#38-purchase-return-register)
  - [3.9 Purchase Matrix](#39-purchase-matrix)
  - [3.10 Purchase Brokerage Report](#310-purchase-brokerage-report)
  - [3.11 Majuri Report (Purchase Majuri)](#311-majuri-report-purchase-majuri)
  - [3.12 Purchase Report (Purchase Quality Report)](#312-purchase-report-purchase-quality-report)
- [4. Sales](#4-sales)
  - [4.1 Journal Sales](#41-journal-sales)
  - [4.2 Journal Sales Report](#42-journal-sales-report)
  - [4.3 Sales Invoice (Tax Invoice)](#43-sales-invoice-tax-invoice)
  - [4.4 Sales Invoice Report](#44-sales-invoice-report)
  - [4.5 E-Invoice Print](#45-e-invoice-print)
  - [4.6 Sales Return](#46-sales-return)
  - [4.7 Sales Return Report](#47-sales-return-report)
  - [4.8 Sales Register](#48-sales-register)
  - [4.9 SalesMan Report](#49-salesman-report)
  - [4.10 Sales Report (Sales Quality Report)](#410-sales-report-sales-quality-report)
- [5. Accounting](#5-accounting)
  - [5.1 Voucher (Receipt / Payment / Contra / Journal)](#51-voucher-receipt--payment--contra--journal)
  - [5.2 Receipt Voucher Multi](#52-receipt-voucher-multi)
  - [5.3 Voucher Report ( Receipt / Payment / Contra / Journal)](#53-voucher-report--receipt--payment--contra--journal)
  - [5.4 Settlement](#54-settlement)
  - [5.5 Ledger](#55-ledger)
  - [5.6 Matrix Outstanding](#56-matrix-outstanding)
  - [5.7 Matrix](#57-matrix)
  - [5.8 Cash (Cash Statement)](#58-cash-cash-statement)
  - [5.9 Cash Register](#59-cash-register)
  - [5.10 Bank (Cheque Deposit)](#510-bank-cheque-deposit)
  - [5.11 Bank Register](#511-bank-register)
  - [5.12 Bank Reco Auto (Bank Reconciliation)](#512-bank-reco-auto-bank-reconciliation)
  - [5.13 Interest Ledger](#513-interest-ledger)
  - [5.14 Multi JV (Journal Voucher Entries)](#514-multi-jv-journal-voucher-entries)
- [6. Inventory](#6-inventory)
  - [6.1 Stock Detail](#61-stock-detail)
  - [6.2 Stock Matrix](#62-stock-matrix)
  - [6.3 Stock Journal](#63-stock-journal)
  - [6.4 Stock Report](#64-stock-report)
  - [6.5 Stock Journal Report](#65-stock-journal-report)
  - [6.6 Stock Transfer](#66-stock-transfer)
  - [6.7 Stock Transfer Report](#67-stock-transfer-report)
  - [6.8 Godown Wise Stock](#68-godown-wise-stock)
- [7. Reports](#7-reports)
  - [7.1 Order Sales Report](#71-order-sales-report)
  - [7.2 Order Purchase Report](#72-order-purchase-report)
  - [7.3 Invoice Sales Report](#73-invoice-sales-report)
  - [7.4 Invoice Purchase Report](#74-invoice-purchase-report)
  - [7.5 Outstanding Sales Report](#75-outstanding-sales-report)
  - [7.6 Brokerage Sales Report](#76-brokerage-sales-report)
  - [7.7 Interest Ledger](#77-interest-ledger)
  - [7.8 Rate Send](#78-rate-send)
  - [7.9 Party Balance](#79-party-balance)
  - [7.10 TCS/TDS Party](#710-tcstds-party)
  - [7.11 TCS Matrix](#711-tcs-matrix)
- [8. Tax](#8-tax)
  - [8.1 GST Summary](#81-gst-summary)
  - [8.2 Form GSTR1](#82-form-gstr1)
  - [8.3 GSTR2](#83-gstr2)
  - [8.4 GSTR2 Reco](#84-gstr2-reco)
  - [8.5 GSTR3B](#85-gstr3b)

## Core Principles & Scope

- **Application Overview:** Dhanhar Masala is an enterprise resource planning (ERP) system designed to manage business operations including multi-branch authentication, real-time sales and purchase logs, complex double-entry accounting, and multi-godown inventory tracking.
- **Document Purpose:** This specification serves as an exhaustive functional layout guide for system architecture, database modeling, and frontend interface design across all active modules.
- **System Conventions:**
  1. Every interactive view contains standard utility controls: a `Heart icon` (favorite toggle) and a `Gear/Settings icon`.
  2. Data tables support sorting per column, export options (Print, PDF, Excel, Envelope/Email), and localized text search.
  3. Ordered lists in this document use `1.` notation for maintainability.

## 1. Authentication & System Scope

### 1.1 Login Page

**Purpose:** Entry point to the system — authenticates users and takes them to Dashboard.

**Fields:**

- **App Code** — text input. Likely a company/tenant identifier (this platform is used by multiple client companies, so App Code tells it which company's data to load). For our build, we probably don't need this — see note below.
- **Username** — text input
- **Password** — text input, masked

**Buttons / Actions:**

- `Login` — submits the form, validates credentials, redirects to Dashboard
- `Scan QR to log in with an app` — alternate login via mobile app QR scan. Skip for v1.
- `Register Face` — face-recognition based login. Skip for v1.

### 1.2 Select Company Page

**Buttons / Actions:**

- `Go` — confirms the selection and takes user into the Dashboard, scoped to that Year + Company + Branch
- `Log out` — top right, exits back to Login page

## 2. Dashboard

### 2.1 Dashboard

**Purpose:** Main landing page after selecting company/branch. Shows overview of business — buyers, orders, money, GST data, sales/purchase trend, and party analysis.

**Fields:**

- **Search box (top, "Party...")**
- **Show entries dropdown** — on Party Analysis table
- **Search box** — inside Party Analysis table

**Buttons / Actions:**

- `Today` — on Money widget
- `Purchase / Sales` — on trend chart
- `Bank Data` — on GST Data widget
- `Party Analysis`
- `Gear/settings icon`
- `Print, Excel` — on Party Analysis table
- `Column sort arrows` — on all Party Analysis columns

### 2.2 Daily Diary

**Purpose:** Date-wise summary of orders, sales, purchases, deliveries, and return cheques.

**Fields:**

- **Date range** — from date, to date

**Buttons / Actions:**

- `GO`
- `Heart icon` — next to heading
- `Gear/settings icon`
- `Person icon` — on each card, opens Voucher Details popup

**Table columns (Return Cheque List):**

| Party Name | Cheque Date | Cheque Reference No | Amount | Deposit Date | Return Date |
| ---------- | ----------- | ------------------- | ------ | ------------ | ----------- |

### 2.3 Voucher Details (popup)

**Purpose:** Opens from the person icon on a Daily Diary card, shows the vouchers behind that card's number.

**Fields:**

- **None**

**Buttons / Actions:**

- `X` — close

**Table columns:**

| SR  | Voucher | Date | Voucher Type | Mode | Party Account | Amount | Remark |
| --- | ------- | ---- | ------------ | ---- | ------------- | ------ | ------ |

### 2.4 Outstanding

**Purpose:** Shows party-wise outstanding balance broken into aging buckets.

**Fields:**

- **Select Type** — dropdown
- **Broker** — dropdown
- **Date range** — from date, to date
- **Bucket range input (0-30, 30-90...)** — near the export icons
- **Show entries dropdown**
- **Search** — inside the table

**Buttons / Actions:**

- `Go`
- `Heart icon` — next to heading
- `Envelope icon`
- `Gear/settings icon`
- `Print, Excel/Excle, Print, Print icons` — export row above table
- `PDF icon, Excel icon` — green icons above table
- `Print, PDF, Excel` — links next to table search
- `Column sort arrows` — on every column
- `Row-level icons (PDF, Print, Excel, Envelope, another icon)` — per party row on the right side

**Table columns:**

| #   | Name | 0-30 | 30-90 | 90-180 | 180-365 | 366+ | Balance | and last column with the row-level icons |
| --- | ---- | ---- | ----- | ------ | ------- | ---- | ------- | ---------------------------------------- |

### 2.5 Pin Board

**Purpose:** A sticky-note style board for jotting down quick notes/reminders.

**Fields:**

- **None visible yet (likely appears after clicking the + to add a note)**

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon - icon` — on the sticky note, likely to add a new note

### 2.6 Analysis (Quality Analysis)

**Purpose:** Shows item-wise sales/stock performance over a date range — how much of each product was sold, stock movement, and active party count.

**Fields:**

- **From date, To date**
- **Search** — inside table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Purchase` — button top right (likely switches this analysis to Purchase side instead of Sales)
- `Submit`
- `Print, PDF, Excel`
- `Column sort arrows` — on every column

**Table columns:**

| SR  | Quality Name | Sold | Material Sold | Material % | Party | Active Party | Party % | Stock In | Stock Out | Stock Sold % |
| --- | ------------ | ---- | ------------- | ---------- | ----- | ------------ | ------- | -------- | --------- | ------------ |

### 2.7 Visit Planning

**Purpose:** Shows planned/missed party visits, day-wise, with future visits also listed.

**Fields:**

- **Search**
- **Date picker**

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Today's Plan`
- `Visit List`
- `Gear/settings icon`
- `Date navigation arrows` — next to the date heading (11-09-2026)
- `Action dropdown` — on each visit card under the date column

**Data shown:**

- Missed Order column — party cards with two dates and a number badge
- Date column (e.g. 11-09-2026) — party cards with a date, two number badges (one green, one blue "Normal"), and Action dropdown
- Future column — empty in this view

### 2.8 Party Visit Plan List

**Purpose:** Opens from Today's Plan / Visit List — shows visit plan entries in table form.

**Fields:**

- **Show entries dropdown**
- **Search**
- **Date picker**

**Buttons / Actions:**

- `Heart icon`
- `Gear/settings icon`
- `Visit Planing` — button top right
- `Previous, Next, page number` — pagination
- `Rupee icon, pencil/edit icon` — per row on the right

**Table columns:**

| SR  | Name | Visit Type | Purpose | Assigned/Call To | Mobile No | Status |
| --- | ---- | ---------- | ------- | ---------------- | --------- | ------ |

### 2.9 Party Detail (opens on clicking a record)

**Purpose:** Shows full detail for a party — contact info, quick action buttons, sales summary, and ledger.

**Fields:**

- **Search box (top, shows "sund"** — party name search)
- **Date range** — from date, to date (for Ledger section)

**Buttons / Actions:**

- `Gear/settings icon`
- `Receipt, Payment, Invoice, Return, Order, Ledger, Outstanding, Quality, Sales Qty` — action buttons
- `GO` — next to Ledger date range
- `Print, file/document, Excel, Envelope, WhatsApp icons` — next to party name in Ledger table

**Data shown (left panel):** - Party name, Pay Day, address, contact person name, mobile number, email, GST number (two codes shown), sales amount, amount due, credit limit %, return goods amount, a small trend chart (line graph, months on x-axis)

**Table columns (Ledger, right panel):**

| Date | LFNO | Particular | Remark | Ref Detail | Ref No | Debit | Credit | Balance Closing Balance row and Total row at the bottom |
| ---- | ---- | ---------- | ------ | ---------- | ------ | ----- | ------ | ------------------------------------------------------- |

### 2.10 Party Zoom (Buyer Zoom)

**Purpose:** Visual box/tile view of parties (buyer/supplier/broker/quality), color-coded, each box clickable to show order history.

**Fields:**

- **None visible**

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Buyer, Supplier, Broker, Quality` — tabs
- `Print icon, Excel icon, Gear/settings icon`
- `Move/arrows icon (below the tab row)`
- `Party boxes (e.g. Shailesh Trading Co, Cash Sales Bhagal, R K Traders, Jai Durga Trading)` — clickable, opens popup

**Data shown:** - Colored tiles, one per party, sized differently, each showing party name

### 2.11 Party Order History (popup)

**Purpose:** Opens on clicking a party tile in Party Zoom — shows that party's order-wise history.

**Fields:**

- **None**

**Buttons / Actions:**

- `X` — close

**Table columns:**

| Order No. | Date | Diff | (unlabeled column with a number badge) | Amount | Diff | (unlabeled column with a highlighted amount badge) |
| --------- | ---- | ---- | -------------------------------------- | ------ | ---- | -------------------------------------------------- |

### 2.12 Price Matrix

**Purpose:** Shows quality-wise price/quantity breakdown, branch-wise, with a unit selector.

**Fields:**

- **Unit dropdown (search box inside it)** — options: KGS, PCS
- **Search** — inside table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Branch tabs` — Bhagal Branch, Bhagal Retail Branch, Devjinagar Retail Branch, Ichhapore Branch, Katargam Main Branch, Katargam Retail Branch
- `Column sort arrows` — on every column

**Table columns:**

| Quality Name | N/A | 0.008 | 0.01 | 0.012 | 0.016 | 0.02 | 0.025 | 0.04 | 0.05 | 0.1 | 0.2 | 0.5 | 1   | 5   | 20 \*\*\*\* |
| ------------ | --- | ----- | ---- | ----- | ----- | ---- | ----- | ---- | ---- | --- | --- | --- | --- | --- | ----------- |

## 3. Purchase

### 3.1 Journal Purchase

**Purpose:** Form to record a purchase transaction, with line items for goods and tax breakdown.

**Fields:**

- **Invoice No.**
- **Invoice Date**
- **Supplier** — dropdown, with a + icon next to it
- **Remark**
- **TDS Applicable** — checkbox
- **Search** — inside the item table, at the bottom
- **Add** — link below search

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Calendar icon` — next to Invoice Date - icon — next to Supplier
- `TCS [%] input, TCS button`
- `Round Off input`
- `Add` — below the table

**Table columns:**

| Name | HSN | GST | Unit | Qty | Rate Per | Rate | Amount | Disc Per | Disc | Taxable | SGST | CGST | IGST | Total |
| ---- | --- | --- | ---- | --- | -------- | ---- | ------ | -------- | ---- | ------- | ---- | ---- | ---- | ----- |

**Bottom rows:** Final Total row, TCS [%] input row, Round Off row

### 3.2 Journal Purchase Report

**Purpose:** Lists all journal purchase entries with filters, totals, and row-level actions.

**Fields:**

- **Date range** — from date, to date
- **Show entries dropdown**
- **Column filter inputs** — Date, Invoice No, Supplier, Taxable, Amount, Remark (under each header)

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Go`
- `Export/print icons` — row of colored icons above the table (multiple, appear to be different export formats)
- `Column sort arrows` — on every column
- `Row-level action icons` — pencil/edit, trash/delete, X (orange), print, question mark/info, upload, download — per row
- `Previous, page numbers (1-6), Next` — pagination

**Table columns:**

| Date | Invoice No | Supplier | Taxable | SGST | CGST | IGST | Amount | Remark | Action |
| ---- | ---------- | -------- | ------- | ---- | ---- | ---- | ------ | ------ | ------ |

**Bottom rows:**

- Page subtotal row (100 entries shown, with column totals)
- Grand Total row (Amount: 0.00)

### 3.3 Purchase Invoice (Tax Invoice)

**Purpose:** Form to create a purchase invoice with quality-wise line items, godown selection, and tax breakdown.

**Fields:**

- **Invoice Type** — radio buttons: Tax Invoice, Bill of Supply, Invoice
- **Account** — dropdown
- **Supplier** — radio + dropdown, with + icon
- **Receiving Goods Address** — radio + dropdown
- **Invoice No.**
- **Invoice Date**
- **Godown** — dropdown
- **Cash Payment** — checkbox
- **Remark**
- **Search** — inside item table, bottom
- **Add** — link below search

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Calendar icon` — next to Invoice Date - icon — next to Supplier
- `Add Quality` — button, above table
- `TCS input, Shipping input, RoundOff input` — bottom right of table
- `Add` — below search

**Table columns:**

| SR  | Quality Name | Qty Per | Unit Sent | Pkg | Qty Sent | Rate Per | Rate | Total | Disc(%) | Disc(Rs) | Freight | SGST | CGST | IGST | Amount |
| --- | ------------ | ------- | --------- | --- | -------- | -------- | ---- | ----- | ------- | -------- | ------- | ---- | ---- | ---- | ------ |

**Bottom row:** Final Total row

### 3.4 Purchase Invoice Report

**Purpose:** Lists purchase invoices with filters, totals, and export options.

**Fields:**

- **Select** — dropdown
- **Select** — dropdown (second one)
- **Date range** — from date, to date
- **All** — dropdown, next to export icons
- **Show entries dropdown**
- **Column filter inputs** — Invoice No, Challan No, Supplier, Unit, Quantity, Taxable, Tax (under headers)

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `New Due, Due` — top right
- `Go`
- `Export icons` — print, Excel, PDF, envelope, print, another export icon (row above table)
- `Column sort arrows` — on every column
- `Previous, Next` — pagination

**Table columns:**

| Date | Invoice No | Challan No | Type | Supplier | Unit | Quantity | Taxable | SGST | CGST | IGST | Tax | Amount | TCS | Action |
| ---- | ---------- | ---------- | ---- | -------- | ---- | -------- | ------- | ---- | ---- | ---- | --- | ------ | --- | ------ |

**Bottom rows:**

- Supplier subtotal row (0, 0, 0.00, 0.00, 0.00, 0.00, 0.00, 0.00)
- Grand Total row — Unit, Quantity, Netmeter, Amount, Taxable, SGST, CGST, IGST, Tax, TCS

### 3.5 Purchase Return

**Purpose:** Form to record a purchase return, credit note, or debit note against a supplier invoice.

**Fields:**

- **Return Type** — radio buttons: Purchase Return, Credit Note, Debit Note
- **Account** — dropdown
- **Prefix**
- **Credit Note No.**
- **Date**
- **Supplier** — radio + dropdown
- **Broker** — dropdown
- **Haste** — radio + dropdown
- **Receiving Goods Address** — radio + dropdown
- **Invoice No.** — dropdown (Select Some Options)
- **Godown** — dropdown
- **Transporter** — dropdown
- **Other Transporter**
- **LR No.**
- **Bale Marka**
- **Remark**
- **Search** — inside item table, bottom

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Calendar icon` — next to Date
- `TCS [%] input, TCS toggle/button`
- `Round Off input`

**Table columns:**

| SR  | Quality Name | HSN | GST | Unit | Qty Per | Quantity | Unit Sent | Quantity Sent | Rate Per | Rate | Amount | Disc(%) | Disc(Rs) | Taxable Value | SGST | CGST | IGST | Total Amount |
| --- | ------------ | --- | --- | ---- | ------- | -------- | --------- | ------------- | -------- | ---- | ------ | ------- | -------- | ------------- | ---- | ---- | ---- | ------------ |

**Bottom rows:** Round Off row, Final Total row

### 3.6 Purchase Return Report

**Purpose:** Lists purchase return/credit note/debit note entries with filters and totals.

**Fields:**

- **Return Type** — radio buttons: Purchase Return, Purchase Credit Note, Purchase Debit Note
- **Date range** — from date, to date
- **Show entries dropdown**
- **Search** — inside table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Go`
- `Export icons` — print, Excel, PDF, envelope, print, another export icon (row above table)
- `Print icon` — second row, standalone
- `Column sort arrows` — on every column
- `Previous, Next` — pagination

**Table columns:**

| Credit Note No | Date | Supplier | Invoice No | Unit | Quantity | Total Taxable | Total | Action |
| -------------- | ---- | -------- | ---------- | ---- | -------- | ------------- | ----- | ------ |

**Bottom rows:**

- Subtotal row (0, 0.00, 0.00, 0.00, 0.00)
- Grand Total row — Unit, Quantity, Netmeter, Taxable Amount, Amount

### 3.7 Purchase Register

**Purpose:** Month-wise summary of purchases with tax breakdown, plus a bar chart visualization.

**Fields:**

- **All** — dropdown
- **Select** — dropdown
- **All Branch** — dropdown
- **All Head** — dropdown
- **ALL** — dropdown
- **Date range** — from date, to date

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Export icons` — print, PDF, Excel, envelope (row above table)
- `Print icon, Excel icon` — per row, right side
- `Scroll-to-top arrow` — bottom left

**Table columns:**

| #   | Month | Taxable | CGST | SGST | IGST | Tax | Amount | Total | Action |
| --- | ----- | ------- | ---- | ---- | ---- | --- | ------ | ----- | ------ |

**Data shown (below table):** - Bar chart — monthly totals, April through March on x-axis

### 3.8 Purchase Return Register

**Purpose:** Month-wise summary of purchase returns with a bar chart visualization.

**Fields:**

- **Select** — dropdown
- **Date range** — from date, to date

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Go`
- `Export icons` — print, Excel (row above table)

**Table columns:**

| #   | Month | Taxable | Tax | Amount | Total |
| --- | ----- | ------- | --- | ------ | ----- |

**Bottom row:** Total row

**Data shown (below table):** - Bar chart — monthly totals, April through March on x-axis

### 3.9 Purchase Matrix

**Purpose:** Shows quality-wise purchase quantity/amount breakdown by unit size, with a unit selector.

**Fields:**

- **Unit dropdown (search box inside it)** — options: KGS, PCS
- **Search** — top right, partially visible

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Column sort arrows` — on every column

**Table columns:**

| Quality Name | N/A | 0.008 | 0.01 | 0.012 | 0.016 | 0.02 | 0.025 | 0.04 | 0.05 | 0.1 | 0.2 | 0.5 | 1   | 5   | 20  | Total |
| ------------ | --- | ----- | ---- | ----- | ----- | ---- | ----- | ---- | ---- | --- | --- | --- | --- | --- | --- | ----- |

### 3.10 Purchase Brokerage Report

**Purpose:** Shows brokerage-wise purchase transactions with received/pending amounts.

**Fields:**

- **Broker/Party dropdown (search box inside it)** — options include Bagreeji Smart Products LLP, R K Masala, Sunfab Designer Shirting, 1 AK Cash Sale Retail Katargam, 1 Devjinagar Cash Retail, 2 AK Cash Sale Wholesaler Katargam, 2 Devjinagar Cash Wholesaler, and phone-number-named entries
- **Date range** — from date, to date
- **Show entries dropdown**
- **Search** — inside table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `GO`
- `Print icon`
- `Column sort arrows` — on every column
- `Previous, Next` — pagination

**Table columns:**

| Date | Invoice | Buyer | Unit | Quantity | Amount | Rec/Ret | Pending |
| ---- | ------- | ----- | ---- | -------- | ------ | ------- | ------- |

### 3.11 Majuri Report (Purchase Majuri)

**Purpose:** Shows majuri (labor charge) figures grouped under Sales, Purchase, Sales Return, and Purchase Return sections.

**Fields:**

- **Date range** — from date, to date

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `GO`
- `Print icon`
- `Scroll-to-top arrow` — bottom left

**Sections shown (each currently empty, no data/table visible):**

- Sales
- Purchase
- Sales Return
- Purchase Return

### 3.12 Purchase Report (Purchase Quality Report)

**Purpose:** Lists purchase transactions quality-wise with tax breakdown.

**Fields:**

- **Select** — dropdown
- **All** — dropdown
- **All** — dropdown (second one)
- **ALL** — dropdown (top right)
- **Date range** — from date, to date
- **Show entries dropdown**
- **Column filter inputs** — Date, Invoice No, Supplier Name, Quality Name, Qty, Rate, CGST, SGST, IGST, Taxable Value, Invoice Value, Transporter Name (under headers)
- **Search** — inside table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `GO`
- `Export icons` — print, Excel, PDF, envelope (row above table)
- `Print` — link next to table search
- `Column sort arrows` — on every column
- `Previous, page numbers (1-6), Next` — pagination
- `Scroll-to-top arrow` — bottom left

**Table columns:**

| Date | Invoice No | Supplier Name | Quality Name | Qty | Rate | CGST | SGST | IGST | Taxable Value | Invoice Value | Transporter Name |
| ---- | ---------- | ------------- | ------------ | --- | ---- | ---- | ---- | ---- | ------------- | ------------- | ---------------- |

**Bottom rows:**

- Page subtotal row (Qty, CGST, SGST, IGST, Taxable Value, Invoice Value totals)
- Grand Total row — Taka, TCS Amount, Invoice Value

## 4. Sales

### 4.1 Journal Sales

**Purpose:** Form to record a sales transaction, with line items for goods and tax breakdown.

**Fields:**

- **Prefix**
- **Invoice No.**
- **LF No.**
- **Invoice Date**
- **Buyer** — dropdown, with + icon next to it
- **Credit Days**
- **Remark**
- **Search** — inside item table, bottom

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Calendar icon` — next to Invoice Date - icon — next to Buyer
- `Round Off input`

**Table columns:**

| Name | HSN | GST | Unit | Qty | Rate Per | Rate | Amount | Disc | Taxable | SGST | CGST | IGST | Total |
| ---- | --- | --- | ---- | --- | -------- | ---- | ------ | ---- | ------- | ---- | ---- | ---- | ----- |

**Bottom rows:** Round Off row, Final Total row

### 4.2 Journal Sales Report

**Purpose:** Lists all journal sales entries with filters, totals, and row-level actions.

**Fields:**

- **Select** — dropdown
- **Date range** — from date, to date
- **Show entries dropdown**
- **Search** — inside table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Go`
- `Export icons` — print, Excel, PDF, print, another export icon (row above table)
- `Column sort arrows` — on every column
- `Previous, Next` — pagination

**Table columns:**

| Date | Invoice No | Buyer | SGST | CGST | IGST | Amount | Action |
| ---- | ---------- | ----- | ---- | ---- | ---- | ------ | ------ |

**Bottom rows:**

- Subtotal row (0, 0, 0, 0)
- Grand Total row (Amount: 0.00)

### 4.3 Sales Invoice (Tax Invoice)

**Purpose:** Form to create a sales invoice with quality-wise line items, delivery details, and tax breakdown.

**Fields:**

- **Challan Type** — radio buttons: Tax Invoice, Bill of Supply, Invoice
- **Account** — dropdown
- **Buyer** — radio + dropdown, with + icon
- **Haste** — radio + dropdown
- **Delivery Party Godown** — radio + dropdown
- **Delivery Days**
- **Remark**
- **Invoice No.**
- **Invoice Date**
- **Godown** — dropdown
- **Transporter** — dropdown, with + icon
- **Other Transporter**
- **Vehicle No.**
- **Transport Paid** — checkbox
- **Cash Payment** — checkbox
- **Search** — top right, above item table
- **Search** — inside item table, bottom
- **Add** — link below search

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Calendar icon` — next to Invoice Date - icon — next to Buyer, next to Transporter
- `CashReceive input`
- `CashBack field (display)`

**Table columns:**

| SR  | Quality Name | GST | Unit Sent | Pkg | Qty Sent | Rate | Help | Total | Disc(%) | Disc(Rs) | Freight | Taxable | SGST | CGST | Total |
| --- | ------------ | --- | --------- | --- | -------- | ---- | ---- | ----- | ------- | -------- | ------- | ------- | ---- | ---- | ----- |

**Bottom rows:** Round Off row, Final Total row

### 4.4 Sales Invoice Report

**Purpose:** Lists sales invoices with filters, totals, and export options.

**Fields:**

- **Select** — dropdown
- **Select** — dropdown (second one)
- **Date range** — from date, to date
- **All** — dropdown, next to export icons
- **Show entries dropdown**
- **Column filter inputs** — Invoice No, Date, Buyer, Quantity, Taxable, CGST, SGST, IGST, Amount (under headers)

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Due, New Due` — top right
- `Print icon` — top right, standalone
- `Go`
- `Export icons` — multiple colored icons (row above table)
- `Column sort arrows` — on every column
- `Previous, Next` — pagination

**Table columns:**

| Invoice No | Date | Buyer | GSTN | Quantity | Taxable | CGST | SGST | IGST | Amount | Action |
| ---------- | ---- | ----- | ---- | -------- | ------- | ---- | ---- | ---- | ------ | ------ |

**Bottom rows:**

- Subtotal row (0, 0.00, 0.00, 0.00, 0.00, 0.00)
- Total row — Total Rolls, Total Meter, Total Netmeter, Total Amount

### 4.5 E-Invoice Print

**Purpose:** Lists sales invoices with e-invoice (IRN/ACK) related fields for e-invoice generation/printing.

**Fields:**

- **Select** — dropdown
- **Select** — dropdown (second one)
- **Date range** — from date, to date
- **All** — dropdown, next to export icons
- **Show entries dropdown**
- **Column filter inputs** — Invoice No, Transporter, Date, Buyer, Amount (under headers)

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Due` — top right
- `Go`
- `Export icons` — multiple colored icons (row above table)
- `Column sort arrows` — on every column
- `Previous, Next` — pagination

**Table columns:**

| Invoice No | Transporter | Date | Buyer | GSTN | Amount | ACK No | ACK Date | Distance | Action |
| ---------- | ----------- | ---- | ----- | ---- | ------ | ------ | -------- | -------- | ------ |

**Bottom rows:**

- Subtotal row
- Total row — Total Rolls, Total Meter, Total Netmeter, Total Amount

### 4.6 Sales Return

**Purpose:** Form to record a sales return, credit note, or debit note against a buyer invoice.

**Fields:**

- **Return Type** — radio buttons: Sales Return, Credit Note, Debit Note
- **Account** — dropdown
- **Prefix**
- **Credit Note No.**
- **Date**
- **Buyer** — radio + dropdown
- **Haste** — radio + dropdown
- **Broker** — dropdown
- **Delivery Party Godown** — radio + dropdown
- **Invoice No.** — dropdown (Select Some Options)
- **Godown** — dropdown
- **Transporter** — dropdown
- **Other Transporter**
- **LR No.**
- **Remark**
- **Without Inventory** — checkbox
- **Cash Payment** — checkbox
- **Document No.**
- **Document Date**
- **Search** — inside item table, bottom

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Calendar icon` — next to Date, next to Document Date

**Table columns:**

| SR  | Quality Name | HSN | GST | Unit | Qty Per | Qty | Unit Received | Quantity Received | Rate Per | Rate | Amount | Disc(%) | Disc(Rs) | Taxable Value | SGST | CGST | IGST | Total Amount |
| --- | ------------ | --- | --- | ---- | ------- | --- | ------------- | ----------------- | -------- | ---- | ------ | ------- | -------- | ------------- | ---- | ---- | ---- | ------------ |

**Bottom rows:** Round Off row, Final Total row

### 4.7 Sales Return Report

**Purpose:** Lists sales return/credit note/debit note entries with filters and totals.

**Fields:**

- **Return Type** — radio buttons: Sales Return, Sales Credit Note, Sales Debit Note
- **ALL** — dropdown
- **Date range** — from date, to date
- **Show entries dropdown**
- **Search** — inside table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Go`
- `Export icons` — multiple colored icons (row above table)
- `Column sort arrows` — on every column
- `Previous, Next` — pagination

**Table columns:**

| No  | Date | Buyer | Quality Name | Haste | Broker | Invoice No | Unit | Quantity | Total Taxable | Total | ACKNO | ACKDate | Quality Remark | Action |
| --- | ---- | ----- | ------------ | ----- | ------ | ---------- | ---- | -------- | ------------- | ----- | ----- | ------- | -------------- | ------ |

**Bottom rows:**

- Subtotal row (0.00, 0.00, 0.00, 0.00)
- Total row — Total Unit, Total Quantity, Total Netmeter, Total Taxable Amount, Total Amount

### 4.8 Sales Register

**Purpose:** Month-wise summary of sales with tax breakdown, plus a bar chart visualization.

**Fields:**

- **All** — dropdown
- **Select Account** — dropdown
- **Select** — dropdown
- **All Branch** — dropdown
- **Date range** — from date, to date

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Go`
- `Export icons` — print, PDF, envelope (row above table)
- `Print icon` — per row, right side
- `Scroll-to-top arrow` — bottom left

**Table columns:**

| #   | Month | Taxable | CGST | SGST | IGST | Tax | Amount | Total | Action |
| --- | ----- | ------- | ---- | ---- | ---- | --- | ------ | ----- | ------ |

**Data shown (below table):** - Bar chart — monthly totals, April through March on x-axis

### 4.9 SalesMan Report

**Purpose:** Shows salesman-wise sales transactions with received/pending amounts.

**Fields:**

- **Select** — dropdown
- **Date range** — from date, to date

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `GO`
- `Export icons` — print, PDF, Excel, envelope (row above table)
- `Column filter inputs` — under each header

**Table columns:**

| Date | Invoice | Buyer | Unit | Quantity | Amount | Rec/Ret | Pending |
| ---- | ------- | ----- | ---- | -------- | ------ | ------- | ------- |

### 4.10 Sales Report (Sales Quality Report)

**Purpose:** Lists sales transactions quality-wise with tax breakdown.

**Fields:**

- **Select** — dropdown
- **All** — dropdown
- **Select** — dropdown (second)
- **All** — dropdown (second)
- **Date range** — from date, to date
- **Show entries dropdown**
- **Column filter inputs** — Date, Invoice No, Buyer Name, GSTN, Quality Name, Qty, Kg, Kg, Rate, Discount %, Discount Rs., Taxable Value (under headers)

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `GO`
- `Export icons` — multiple colored icons, two rows (print, Excel, PDF, envelope, print, more)
- `Print` — link next to table
- `Column sort arrows` — on every column
- `Previous, page numbers (1-5, ..., 1239), Next` — pagination
- `Scroll-to-top arrow` — bottom left

**Table columns:**

| Date | Invoice No | Buyer Name | GSTN | Quality Name | Quality Type | Qty | Kg  | Kg  | Rate | Discount % | Discount Rs. | Taxable Value | CGST | SGST (more columns likely continue beyond visible area) |
| ---- | ---------- | ---------- | ---- | ------------ | ------------ | --- | --- | --- | ---- | ---------- | ------------ | ------------- | ---- | ------------------------------------------------------- |

**Bottom rows:**

- Page subtotal row (Qty, Kg, Kg, Discount Rs., Taxable Value totals)
- Grand Total row — Taka, Meter, Kg, Discount Rs., Taxable Value, Invoice Value

## 5. Accounting

### 5.1 Voucher (Receipt / Payment / Contra / Journal)

**Purpose:** Single form to record accounting vouchers, with tabs switching between Receipt, Payment, Contra, and Journal types. TDS section appears when applicable.

_Receipt tab_

- **Voucher No.**
- **Voucher Date**
- **Transaction Type** — dropdown (e.g. Net Banking)
- **Party Account** — dropdown, with + icon
- **Bank Account** — dropdown (shows balance, e.g. "7717701.59 DR")
- **Ref No.**
- **Ref Date**
- **Amount**
- **Remark**
- **TDS Applicable** — checkbox

_Payment tab_

- **Voucher No.**
- **Voucher Date** — with calendar picker (shown open with month navigation, Today button)
- **Transaction Type** — dropdown (e.g. Net Banking)
- **Party Account** — dropdown, with + icon
- **Bank Account** — dropdown (shows balance, e.g. "7717701.59 DR")
- **Chq/NEFT Ref No.**
- **Chq/NEFT Date**
- **Amount**
- **Remark**
- **TDS Applicable** — checkbox
- **(When TDS checked) Amount Per TDS, TDS Account** — dropdown, Nature Of Payment — dropdown, Status — dropdown, Applicable Rate, TDS

_Contra tab_

- **Voucher No.**
- **LF No.**
- **Voucher Date**
- **Voucher Type** — dropdown (e.g. Cash Deposit)
- **From Account** — dropdown, with + icon (shows balance, e.g. "848547.62 DR")
- **To Account** — dropdown
- **Amount**
- **Print** — checkbox
- **Remark**

_Journal tab_

- **Voucher No.**
- **LF No.**
- **Voucher Date**
- **Transaction Type** — dropdown (e.g. Journal Voucher)
- **Debit Party Account** — radio + dropdown, with + icon
- **Credit Party Account** — radio + dropdown
- **Amount**
- **Remark**
- **TDS Applicable** — checkbox
- **(When TDS checked) TDS Account, Nature Of Payment, Status, Applicable Rate, TDS**

_Common across all tabs_

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Multi Payment Voucher / Multi Journal Voucher` — top right (tab-specific label)
- `Calendar icon` — next to date fields - icon — next to account dropdowns -

### 5.2 Receipt Voucher Multi

**Purpose:** Bulk entry screen for recording multiple receipt/payment/journal vouchers at once.

**Fields:**

- **Voucher Type** — tabs: Receipt, Payment, Journal
- **Enter No.**
- **Voucher Date**
- **Transaction Type** — dropdown
- **Show TDS Section** — checkbox
- **Cash Account** — dropdown
- **Total Amount**

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Go`
- `Submit`

**Table columns:**

| Voucher: # | Voucher: Voucher No | Voucher: LF No | Voucher: Party | Voucher: Amount | Voucher: Remarks | Tran Detail: Ref No | Tran Detail: Ref Date |
| ---------- | ------------------- | -------------- | -------------- | --------------- | ---------------- | ------------------- | --------------------- |

**Additional table columns shown when "Show TDS Section" is checked:** Three grouped sections now — Voucher: #, Voucher No, LF No, Party, Amount, Remarks — Tran Detail: Ref No, Ref Date — TDS Detail: TDS Applicable, Amount Per TDS, TDS Account, Nature Of Payment, Status, Applicable Rate, TDS

| Voucher: # | Voucher: Voucher No | Voucher: LF No | Voucher: Party | Voucher: Amount | Voucher: Remarks | Tran Detail: Ref No | Tran Detail: Ref Date | TDS Detail: TDS Applicable | TDS Detail: Amount Per TDS | TDS Detail: TDS Account | TDS Detail: Nature Of Payment | TDS Detail: Status | TDS Detail: Applicable Rate | TDS Detail: TDS |
| ---------- | ------------------- | -------------- | -------------- | --------------- | ---------------- | ------------------- | --------------------- | -------------------------- | -------------------------- | ----------------------- | ----------------------------- | ------------------ | --------------------------- | --------------- |

### 5.3 Voucher Report ( Receipt / Payment / Contra / Journal)

**Purpose:** Lists recorded vouchers, tab-switchable by voucher type, with filters, totals, and row-level actions.

_Receipt tab_

- **Select PartyBroker**
- **Select** — dropdown (Report Print / Report View / VoucherPrint InvoiceSet)
- **Date range** — from date, to date
- **Show entries dropdown**
- **Search** — inside table
- **Column filter inputs** — VoucherNo, VoucherDate, VoucherType, TxnType, Bank, Party, City, ChequeNo, Amount, Remark (under headers)

_Payment tab_

- **Select PartyBroker**
- **Select** — dropdown (Select / Cash / Bank / Net Banking)
- **Date range** — from date, to date
- **Show entries dropdown**
- **Search** — inside table
- **Column filter inputs** — same as Receipt

_Contra tab_

- **Date range** — from date, to date
- **Show entries dropdown**
- **Search** — inside table
- **Column filter inputs** — VoucherNo, VoucherDate, VoucherType, DebitParty, CreditParty, Amount, Remark

_Journal tab_

- **Date range** — from date, to date
- **Show entries dropdown**
- **Search** — inside table
- **Column filter inputs** — VoucherNo, VoucherDate, VoucherType, DebitParty_Name, CreditParty_Name, Amount, Remark

_Common across all tabs_

- `Heart/list icon, Gear/settings icon`
- `Print icon, PDF icon, Excel icon` — top right
- `Report Print / Default` — dropdowns, top right
- `Go`
- `CSV, Excel, PDF, Print` — links next to search
- `Column sort arrows` — on every column
- `Row-level action icons` — expand, delete, X, print, info, upload, download, envelope, another icon (varies slightly per tab) — per row
- `Previous, Next` — pagination (Receipt/Payment tabs)

**Table columns (Receipt tab):**

| VoucherNo | VoucherDate | VoucherType | TxnType | Bank | Party | City | ChequeNo | Amount | Remark | Action |
| --------- | ----------- | ----------- | ------- | ---- | ----- | ---- | -------- | ------ | ------ | ------ |

**Table columns (Payment tab):**

| Same as Receipt |
| --------------- |

**Table columns (Contra tab):**

| VoucherNo | VoucherDate | VoucherType | DebitParty | CreditParty | Amount | Remark | Action |
| --------- | ----------- | ----------- | ---------- | ----------- | ------ | ------ | ------ |

**Table columns (Journal tab):**

| VoucherNo | VoucherDate | VoucherType | DebitParty_Name | CreditParty_Name | Amount | Remark | Action |
| --------- | ----------- | ----------- | --------------- | ---------------- | ------ | ------ | ------ |

**Bottom row (Receipt/Payment tabs):** Amount total row

### 5.4 Settlement

**Purpose:** Lets a party's transactions (invoices, receipts, payments) be settled against each other, split into Settled and Un Settled sections.

**Fields:**

- **Party dropdown (search box inside it)** — options include Bagreeji Smart Products LLP, Cash Bhagal, R K Masala, Sunfab Designer Shirting, and several other named parties

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Print icon`
- `Submit`
- `Three number values shown top right (00000, 00000, 00000)` — likely summary figures, labels not visible

**Sections shown:**

- Settled (left, empty in this view)
- Un Settled (right, empty in this view)

### 5.5 Ledger

**Purpose:** Shows a party's full transaction ledger — debit/credit entries with running balance.

**Fields:**

- **Party** — dropdown
- **Date range** — from date, to date
- **Show entries dropdown**
- **Search** — inside table

**Buttons / Actions:**

- `Gear/settings icon`
- `Export icons` — multiple (print, Excel, PDF, print, envelope — row above table)
- `GO`
- `Column sort arrows` — on every column
- `Previous, page number, Next` — pagination

**Table columns:**

| SR  | Date | LFNO | Particular | Remark | Ref Detail | Ref No | Debit | Credit | Balance |
| --- | ---- | ---- | ---------- | ------ | ---------- | ------ | ----- | ------ | ------- |

**Rows shown:** Opening Balance row, Closing Balance row, Total row (Debit, Credit, Balance)

### 5.6 Matrix Outstanding

**Purpose:** Summary view showing outstanding totals split into Debtors (Sales side) and Creditors (Purchase side).

**Fields:**

- **None visible**

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`

**Table columns (Debtors):**

| Name | Grand Total |
| ---- | ----------- |

_Rows: Sales, Receive, Current Month, Old Month, Debtors_

**Table columns (Creditors):**

| Name | Grand Total |
| ---- | ----------- |

_Rows: Purchase, Payment, Current Month, Old Month, Creditors_

### 5.7 Matrix

**Purpose:** Shows a broker-wise breakdown for a selected transaction type (Receipt Voucher, Payment Voucher, Sales, Sales Return, Sales Journal, Purchase, Purchase Return, Purchase Journal, Direct Indirect).

**Fields:**

- **Type dropdown (search box inside it)** — options: Direct Indirect, Receipt Voucher, Payment Voucher, Sales, Sales Return, Sales Journal, Purchase, Purchase Return, Purchase Journal
- **Show entries dropdown**
- **Search** — inside table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Go`
- `Excel, PDF, Print` — links next to search
- `Column sort arrows` — on every column
- `Previous, Next` — pagination

**Table columns:**

| SR  | Name | Broker | Grand Total |
| --- | ---- | ------ | ----------- |

**Bottom row:** Total row

### 5.8 Cash (Cash Statement)

**Purpose:** Shows day-wise cash transactions with running balance.

**Fields:**

- **Account dropdown (e.g. Cash)**
- **Date range** — from date, to date
- **Show entries dropdown**
- **Search** — inside table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `GO`
- `Column sort arrows` — on every column

**Table columns:**

| SR  | Voucher Date | Particulars | Voucher Type | Voucher No | Transaction Type | Debit | Credit | Balance |
| --- | ------------ | ----------- | ------------ | ---------- | ---------------- | ----- | ------ | ------- |

**Rows shown:** Opening Balance row

### 5.9 Cash Register

**Purpose:** Month-wise cash summary with running balance, plus a bar chart visualization.

**Fields:**

- **Account dropdown (e.g. Cash)**

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Export icons` — print, PDF, Excel (top right)
- `Print icon` — per row, right side

**Table columns:**

| #   | Month | Debit | Credit | Amount | Action |
| --- | ----- | ----- | ------ | ------ | ------ |

**Rows shown:** Opening Balance row

**Data shown (below table):** - Bar chart — monthly totals, April through March on x-axis

### 5.10 Bank (Cheque Deposit)

**Purpose:** Drag-and-drop interface to move cheques between Cleared and Return status.

**Fields:**

- **Date picker**

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `GO`

**Sections shown (drag-and-drop zones):**

- Cleared Cheque List — with date shown per zone (31-03-2024)
- Cheque Return List — with date shown per zone (31-03-2024)

### 5.11 Bank Register

**Purpose:** Month-wise bank account summary with running balance, plus a bar chart visualization.

**Fields:**

- **Account dropdown (search box inside it)** — options: Axis Bank, Bank Of Baroda, HDFC Bank, KMBL

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Print icon` — top right
- `Print icon` — per row, right side

**Table columns:**

| #   | Month | Debit | Credit | Amount | Action |
| --- | ----- | ----- | ------ | ------ | ------ |

**Rows shown:** Opening Balance row

**Data shown (below table):** - Bar chart — monthly totals (positive and negative values), April through March on x-axis

### 5.12 Bank Reco Auto (Bank Reconciliation)

**Purpose:** Reconciles bank transactions against system-recorded vouchers, using an uploaded bank statement file with three related tables.

**Fields:**

- **Party/Broker dropdown**
- **Choose file** — file upload input (bank statement)

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Auto Reco`
- `Expand/fullscreen icon` — top right of table area

**Table columns:**

| SR  | Date | Voucher Type | Transaction Type | Chq/Ref | Deposited Date | Debit | Credit | Old Reco | New Reco | Bank Remark |
| --- | ---- | ------------ | ---------------- | ------- | -------------- | ----- | ------ | -------- | -------- | ----------- |

**Table columns:**

| SR  | Date | Particulars | Chq/Ref | Debit | Credit |
| --- | ---- | ----------- | ------- | ----- | ------ |

**Table columns:**

| SR  | Date | Voucher Type | Transaction Type | Chq/Ref | Deposited Date | Debit | Credit |
| --- | ---- | ------------ | ---------------- | ------- | -------------- | ----- | ------ |

### 5.13 Interest Ledger

**Purpose:** Calculates interest on a party's outstanding balance based on debit/credit rate percentages over a date range.

**Fields:**

- **Select Party** — dropdown
- **Start Date**
- **End Date**
- **Dr %**
- **Cr %**
- **Enter Days**
- **Gp Dr**
- **Gp Cr**

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `GO`
- `Print, Excel`

**Table columns:**

| Name | Balance |
| ---- | ------- |

**Rows shown:** Total, Interest, Total With Interest

### 5.14 Multi JV (Journal Voucher Entries)

**Purpose:** Bulk entry screen for multi-line journal vouchers with debit/credit type selection.

**Fields:**

- **Voucher number input**
- **Select** — dropdown
- **Dr/Cr dropdown (search box inside it)** — options: Dr, Cr
- **Voucher Date**
- **Show entries dropdown**
- **Search** — inside table
- **Name** — dropdown, per row (shown as "SELECT")
- **Amount** — input, per row

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Go`
- `Submit`
- `Previous, page number, Next` — pagination

**Table columns:**

| SR  | Name | Amount \*\*\*\* |
| --- | ---- | --------------- |

## 6. Inventory

### 6.1 Stock Detail

**Purpose:** Shows quality-wise stock movement (opening, bought, sold, closing) per godown, with a godown filter.

**Fields:**

- **Date range** — from date, to date
- **Godown tabs** — All, Bhagal Godown, Ichhapore, Jainam Trade Link LLP, Surat Agro Cold Storage, Uma Akash Agro Pvt.Ltd, Bhagal Retail Godown, Devjinagar Godown, Icchapore P/C, Katargam, Katargam Retail Godown
- **Show entries dropdown**
- **Search** — inside table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `GO`
- `Export icons` — multiple colored icons (row above table)
- `Column sort arrows` — on every column
- `Previous, page numbers (1-5, ..., 50), Next` — pagination

**Table columns:**

| #   | Quality Name | Opening | Bought | Sold | Closing |
| --- | ------------ | ------- | ------ | ---- | ------- |

_(each cell shows two stacked values — likely unit and quantity)_

**Bottom row:** Total Unit, Total Quantity

### 6.2 Stock Matrix

**Purpose:** Shows quality-wise stock quantity breakdown by unit size, per branch-godown combination, with a unit selector.

**Fields:**

- **Unit dropdown (search box inside it)** — options: KGS, PCS
- **Branch-Godown tabs** — All, Bhagal Branch-Bhagal Godown, Bhagal Branch-Ichhapore, Bhagal Branch-Jainam Trade Link LLP, Bhagal Branch-Uma Akash Agro Pvt.Ltd (more tabs likely continue beyond visible area)
- **Search** — inside table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Column sort arrows` — on every column
- `Scroll-to-top arrow` — bottom left

**Table columns:**

| Quality Name | N/A | 0.008 | 0.01 | 0.012 | 0.016 | 0.02 | 0.025 | 0.04 | 0.05 | 0.1 | 0.2 | 0.5 | 1   | 5   | 20  | Total |
| ------------ | --- | ----- | ---- | ----- | ----- | ---- | ----- | ---- | ---- | --- | --- | --- | --- | --- | --- | ----- |

**Bottom row:** Column totals row

### 6.3 Stock Journal

**Purpose:** Form to record a manual stock adjustment/journal entry, converting between sale and purchase quantities per quality.

**Fields:**

- **Voucher No.**
- **Voucher Date**
- **Godown** — dropdown
- **Remark**
- **Search** — top right, above item table
- **Search** — inside item table, bottom

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Calendar icon` — next to Voucher Date

**Fields:**

- **Difference (shows a ratio, e.g. "0 / 0.000")**
- **Voucher Type (shows "Stock Journal Voucher")**

**Table columns:**

| SR  | Quality Name | Sale Unit | Sale Qty | Sales Per | Purchase Unit | Purchase Qty | Sales Per |
| --- | ------------ | --------- | -------- | --------- | ------------- | ------------ | --------- |

**Bottom row:** Total row

### 6.4 Stock Report

**Purpose:** Shows a stock movement summary with three views — All (line-item breakdown), Grey MonthWise, and Finish MonthWise — tracking stock across shop, mill, and reprocessing stages.

**Fields:**

- **Branch** — dropdown (e.g. Bhagal Branch)
- **Date range** — from date, to date
- **View toggle** — radio buttons: All, Grey MonthWise, Finish MonthWise

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon`
- `Go`
- `Export icons` — multiple colored icons (row above table)
- `Row-level export icon (Action column)` — per line, All view only

**Table columns (All view):**

| Description | #   | StockQty | Value | Action |
| ----------- | --- | -------- | ----- | ------ |

_Rows: Opening Grey, Grey Purchase, Grey Purchase Return, Grey Sales, Grey Sales Return, Grey Send To Mill, Grey Return From Mill, (Grey Stock At Shop), Opening At Mill, Grey Send To Mill, Received From Mill, Re-Process To Mill, Received From Re-Process, Grey Return From Mill, Shortage At Mill, Elogated (Excess MTS)_

**Table columns (Grey MonthWise view, first table):**

| Month | (+) Open Grey | (+) Grey Pur. | (-) Grey Pur.Return | (-) Grey Sales | (+) Grey Sales.Return | (-) Send To Mill | (+) Rtn From Mill | (+) Grey From Mill | (=) Grey At Shop |
| ----- | ------------- | ------------- | ------------------- | -------------- | --------------------- | ---------------- | ----------------- | ------------------ | ---------------- |

**Table columns (Grey MonthWise view, second table):**

| Month | (+) Open At Mill | (+) Grey Send To Mill | (+) Refinish | (-) Rec. From Mill | (-) Grey Return From Mill | (-) Grey Receive From Mill | (-) Rec. From Refinish | (-) Loss At Mill | (+) Elogated | (=) Stock At Mill |
| ----- | ---------------- | --------------------- | ------------ | ------------------ | ------------------------- | -------------------------- | ---------------------- | ---------------- | ------------ | ----------------- |

**Table columns (Finish MonthWise view):**

| Month | (+) OpenFinished | (+) FinishPur | (-) FinishPurr | (+) RecdFrmMill | (-) Refinished | (+) ReceiveRefinished | (-) Sales | (+) SalesRtn | (+) Elogated | (=) FinStock |
| ----- | ---------------- | ------------- | -------------- | --------------- | -------------- | --------------------- | --------- | ------------ | ------------ | ------------ |

**Bottom row:** Total row (MonthWise views)

### 6.5 Stock Journal Report

**Purpose:** Lists stock journal entries (quality-wise stock movement records) with sorting, search, and pagination — currently showing no data.

**Navigation:** Home / Accounting / Stock Journal Report (accessed via Inventory → Stock Journal Report in sidebar)

**Fields:**

- **Branch** — shown in top bar (Bhagal Branch), not a page-level filter here
- **Show entries** — dropdown (e.g. 100) controlling rows per page
- **Search** — text box, searches across table

**Buttons / Actions:**

- `Gear/settings icon` — top right
- `Print icon (orange)` — top right
- `Sort arrows` — on each sortable column header
- `Previous / Next` — pagination controls

**Table columns:**

| No  | Date | Quality Name | Unit | Qty | Per | Type | Remark | Action |
| --- | ---- | ------------ | ---- | --- | --- | ---- | ------ | ------ |

### 6.6 Stock Transfer

**Purpose:** Create/manage a stock transfer between godowns — includes transfer details header and a line-item table for quality-wise transfer.

**Navigation:** Home / Inventory / Stock Transfer

**Fields:**

- **Transfer No.** — text/auto-filled (e.g. 1256)
- **Transfer Date** — date picker (e.g. 14-09-2026)
- **From Godown** — dropdown
- **To Godown** — dropdown
- **Transporter** — text
- **LR No.** — text
- **LF No.** — text
- **Driver Name** — text
- **Driver Mob No.** — text
- **Vehicle No.** — text
- **Employee** — text
- **Expense** — text
- **Remark** — textarea
- **Search** — text box (above table, filters table)
- **Search** — text box (below table, secondary filter)

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right

**Table columns:**

| SR  | Quality Name | Units Sent | Quantity Sent | Rate Per |
| --- | ------------ | ---------- | ------------- | -------- |

**Bottom row:** Total row

### 6.7 Stock Transfer Report

**Purpose:** Lists all stock transfer transactions between godowns with quality, quantity, and remark details — sortable, searchable, paginated list.

**Navigation:** Home / Inventory / Stock Transfer Report

**Fields:**

- **Show entries** — dropdown (e.g. 100) controlling rows per page
- **Search** — text box, searches across table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right
- `Print icon (orange)` — top right
- `Print icon (green)` — top right
- `Export icon (green)` — top right
- `Sort arrows` — on Date, Issue For, Quantity columns
- `No (transfer no.)` — clickable link per row, opens that transfer

**Table columns:**

| No  | Date | Quality | Issue For | From | To  | Unit | Quantity | LFNO | Remark |
| --- | ---- | ------- | --------- | ---- | --- | ---- | -------- | ---- | ------ |

### 6.8 Godown Wise Stock

**Purpose:** Shows material-wise opening, purchase, sell, and closing stock (unit, qty, rate, amount) for each godown, with a separate table block per godown.

**Navigation:** Home / Inventory / Godown Wise Stock

**Fields:**

- **No visible filters on this view (godown blocks are shown sequentially for all godowns, e.g. Bhagal Godown, Surat Agro Cold Storage, Uma Akash Agro Pvt.Ltd, Ichhapore)**

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Print icon` — top right
- `Excel export icon` — top right
- `PDF export icon` — top right
- `Gear/settings icon` — top right

**Table columns (per godown block):**

| Material | Opening (Unit | Qty | Rate | Amount) | Purchase (Unit | Qty) | Sell (Unit | Qty) | Closing (Unit | Qty | Rate | Amount) |
| -------- | ------------- | --- | ---- | ------- | -------------- | ---- | ---------- | ---- | ------------- | --- | ---- | ------- |

**Rows:** Hing, Masala, Chilly Powder, Haldi Powder, Dhana Powder, Rajgara Lot, Shingoda Lot, Rock Salt, Amchur Powder, Jira Powder Loose, Mari Powder, Variyali, Rai, Oil, Chilly Powder-PCS, Dry Fruit 5%, Sabudana, Rajgara (list varies slightly per godown)

**Bottom row:** Total row (per godown block)

**Structure:** Multiple godown blocks stacked vertically, each with its own header bar (godown name) and full table.

## 7. Reports

### 7.1 Order Sales Report

**Purpose:** Lists sales orders with drill-down groupings (by Item, Broker, City, Party, or combinations) and status filters (Pending, Ordered, Completed), showing order-level and buyer-level detail with unit, quantity, rate, and value.

**Navigation:** Home / Report / OrderSales

**Fields:**

- **Quality** — multi-select dropdown ("Select Some Options"), filters by item/quality. Appears/disappears depending on which grouping tab is active.
- **Broker** — multi-select dropdown ("Select Some Options"), filters by broker. Appears when grouping includes Broker.
- **City** — multi-select dropdown ("Select Some Options"), filters by city. Appears when grouping includes City.
- **Date range** — from date, to date (e.g. 01-04-2023 to 31-03-2024)
- **Status** — radio buttons: Pending, Ordered, Ordered, Completed
- **Grouping tabs** — button-style toggle group: Item, Broker City, City Broker, Broker Item, Item Broker, City Item, Item City, Broker Party, City Party, Party Item, Item Party
- **Show entries** — dropdown (e.g. 25) controlling rows per page
- **Search** — text box, searches across table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right
- `Print icon` (green) — top right
- `Go` — applies filters and refreshes table
- `Sort arrows` — on sortable column headers
- `Order No` — clickable link per row, opens order detail

**Table columns:**

| Order No | Order Date | Haste | Broker | Buyer | Transporter | City | Quality | Unit | Quantity | Rate | Value |
| -------- | ---------- | ----- | ------ | ----- | ----------- | ---- | ------- | ---- | -------- | ---- | ----- |

**Grouping rows:** When a grouping tab (e.g. Broker City, City Broker) is selected, the table inserts subtotal header rows above each group (e.g. "NO BROKER NAME", "SURAT", "555 HING POWDER 1 KG") showing aggregated Unit, Quantity, and Value for that group before listing individual line items underneath.

---

### 7.2 Order Purchase Report

**Purpose:** Lists purchase orders with drill-down groupings (by Item, Broker, City, Party, or combinations) and status filters (Pending, Ordered, Completed), showing order-level and supplier-level detail with unit, quantity, rate, and value.

**Navigation:** Home / Report / OrderPurchase

**Fields:**

- **Quality** — multi-select dropdown ("Select Some Options"), filters by item/quality. Appears/disappears depending on which grouping tab is active.
- **Broker** — multi-select dropdown ("Select Some Options"), filters by broker. Appears when grouping includes Broker.
- **City** — multi-select dropdown ("Select Some Options"), filters by city. Appears when grouping includes City.
- **Date range** — from date, to date (e.g. 01-04-2023 to 31-03-2024)
- **Status** — radio buttons: Pending, Ordered, Ordered, Completed
- **Grouping tabs** — button-style toggle group: Item, Broker City, City Broker, Broker Item, Item Broker, City Item, Item City, Broker Party, City Party, Party Item, Item Party
- **Show entries** — dropdown (e.g. 25) controlling rows per page
- **Search** — text box, searches across table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right
- `Print icon` (green) — top right
- `Go` — applies filters and refreshes table
- `Sort arrows` — on sortable column headers
- `Order No` — clickable link per row, opens order detail

**Table columns:**

| Order No | Order Date | Haste | Broker | Supplier | Transporter | City | Quality | Unit | Quantity | Rate | Value |
| -------- | ---------- | ----- | ------ | -------- | ----------- | ---- | ------- | ---- | -------- | ---- | ----- |

**Grouping rows:** When a grouping tab (e.g. Broker City, City Broker) is selected, the table inserts subtotal header rows above each group (e.g. "NO BROKER NAME", "SURAT", "NAVI MUMBAI") showing aggregated Unit and Quantity for that group before listing individual line items underneath. With City Broker grouping, city-level subtotals contain nested broker-level subtotals.

---

### 7.3 Invoice Sales Report

**Purpose:** Lists sales invoices with drill-down groupings (by Item, Broker, City, Party, or combinations), showing invoice-level and buyer-level detail with unit, quantity, net meter, taxable amount, and tax breakup (SGST, CGST, IGST).

**Navigation:** Home / Report / InvoiceSales

**Fields:**

- **Quality** — multi-select dropdown ("Select Some Options"), filters by item/quality. Appears/disappears depending on which grouping tab is active.
- **Broker** — multi-select dropdown ("Select Some Options"), filters by broker. Appears when grouping includes Broker.
- **City** — multi-select dropdown ("Select Some Options"), filters by city. Appears when grouping includes City.
- **Date range** — from date, to date (e.g. 01-04-2023 to 31-03-2024)
- **Grouping tabs** — button-style toggle group: Item, Broker City, City Broker, Broker Item, Item Broker, City Item, Item City, Broker Party, City Party, Party Item, Item Party
- **Show entries** — dropdown (e.g. 25) controlling rows per page
- **Search** — text box, searches across table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right
- `Print icon` (green) — top right
- `Go` — applies filters and refreshes table
- `Sort arrows` — on sortable column headers
- `Invoice No` — clickable link per row, opens invoice detail

**Table columns:**

| Invoice No | Bale No | Broker | Invoice Date | Buyer | City | Quality | Unit | Quantity | Net Meter | Taxable Amount | SGST | CGST | IGST | Amount |
| ---------- | ------- | ------ | ------------ | ----- | ---- | ------- | ---- | -------- | --------- | -------------- | ---- | ---- | ---- | ------ |

**Grouping rows:** When a grouping tab (e.g. Broker City) is selected, the table inserts subtotal header rows above each group (e.g. "NO BROKER NAME", "# SURAT") showing aggregated Unit, Quantity, Net Meter, Taxable Amount, SGST, CGST, IGST, and Amount for that group before listing individual line items underneath.

### 7.4 Invoice Purchase Report

**Purpose:** Lists purchase invoices with drill-down groupings (by Item, Broker, City, Party, or combinations), showing invoice-level and supplier-level detail with unit, quantity, net meter, taxable amount, and tax breakup (SGST, CGST, IGST).

**Navigation:** Home / Report / InvoicePurchase

**Fields:**

- **Quality** — multi-select dropdown ("Select Some Options"), filters by item/quality. Appears/disappears depending on which grouping tab is active.
- **Broker** — multi-select dropdown ("Select Some Options"), filters by broker. Appears when grouping includes Broker.
- **City** — multi-select dropdown ("Select Some Options"), filters by city. Appears when grouping includes City.
- **Date range** — from date, to date (e.g. 01-04-2023 to 31-03-2024)
- **Grouping tabs** — button-style toggle group: Item, Broker City, City Broker, Broker Item, Item Broker, City Item, Item City, Broker Party, City Party, Party Item, Item Party
- **Show entries** — dropdown (e.g. 25) controlling rows per page
- **Search** — text box, searches across table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right
- `Print icon` (green) — top right
- `Go` — applies filters and refreshes table
- `Sort arrows` — on sortable column headers
- `Invoice No` — clickable link per row, opens invoice detail

**Table columns:**

| Invoice No | Bale No | Broker | Invoice Date | Supplier | City | Quality | Unit | Quantity | Net Meter | Taxable Amount | SGST | CGST | IGST | Amount |
| ---------- | ------- | ------ | ------------ | -------- | ---- | ------- | ---- | -------- | --------- | -------------- | ---- | ---- | ---- | ------ |

**Grouping rows:** When a grouping tab (e.g. Broker City, Item Broker) is selected, the table inserts subtotal header rows above each group (e.g. "NO BROKER NAME", "# AHMEDABAD", "# NO BROKER NAME") showing aggregated Unit, Quantity, Net Meter, Taxable Amount, SGST, CGST, IGST, and Amount for that group before listing individual line items underneath. With Item Broker grouping, item-level subtotals contain nested broker-level subtotals.

### 7.5 Outstanding Sales Report

**Purpose:** Lists outstanding (unpaid/partially paid) sales invoices with drill-down groupings (by Broker, City, Area, AreaCode, Party), showing receivable, pending, credit days, and overdue days per invoice, grouped by party/broker/city/area blocks.

**Navigation:** Home / Report / Outstanding Sales

**Fields:**

- **Party** — multi-select dropdown ("Select Some Options"), filters by buyer/party
- **Broker** — multi-select dropdown ("Select Some Options"), filters by broker. Appears/disappears depending on which grouping tab is active.
- **City** — multi-select dropdown ("Select Some Options"), filters by city. Appears when grouping includes City.
- **Area** — multi-select dropdown ("Select Some Options"), filters by area. Appears when grouping includes Area.
- **AreaCode** — multi-select dropdown ("Select Some Options"), filters by area code. Appears when grouping includes AreaCode.
- **AccountType** — dropdown ("Select Type"). Appears when grouping includes Area or AreaCode.
- **Date range** — from date, to date (e.g. 01-04-2023 to 31-03-2024)
- **View mode** — radio buttons: SubGroup, Group
- **Grouping tabs** — button-style toggle group: Broker Party, City Party, City Broker, Broker City, Area Party, AreaCode Party
- **Show entries** — dropdown (e.g. 25) controlling rows per page
- **Search** — text box, searches across table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right
- `Print icon` (green) — top right
- `Go` — applies filters and refreshes table
- `Sort arrows` — on sortable column headers

**Table columns:**

| Invoice No | Date | Buyer | Broker | City | Area | AreaCode | Unit | Quantity | Amount | Receive | Pending | Credit Day | Overdue Day | Actual Day |
| ---------- | ---- | ----- | ------ | ---- | ---- | -------- | ---- | -------- | ------ | ------- | ------- | ---------- | ----------- | ---------- |

**Grouping rows:** When a grouping tab is active (e.g. Broker Party), the table inserts a subtotal header row per party (e.g. "VIMAL TRADING CO") showing aggregated Unit, Quantity, Amount, Receive, and Pending for that party before listing individual invoice line items underneath. Empty result sets (e.g. City Broker, Area Party, AreaCode Party groupings in this dataset) show no rows below the header.

### 7.6 Brokerage Sales Report

**Purpose:** Lists brokerage-related sales invoices with drill-down groupings (by Party, Broker, City), showing tax breakup, discount, returns, net amount received, and voucher/cheque details per invoice, grouped by broker/party/city blocks.

**Navigation:** Home / Report / Brokerage Sales

**Fields:**

- **Party** — multi-select dropdown ("Select Some Options"), filters by buyer/party. Appears when grouping includes Party.
- **Broker** — multi-select dropdown ("Select Some Options"), filters by broker. Appears when grouping includes Broker.
- **City** — multi-select dropdown ("Select Some Options"), filters by city. Appears when grouping includes City.
- **Date range** — from date, to date (e.g. 01-04-2023 to 31-03-2024)
- **View mode** — radio buttons: SubGroup, Group
- **Date type** — radio buttons: VoucherDate, ChequeDate
- **Grouping tabs** — button-style toggle group: Broker Party, Party Broker, Broker City, City Broker
- **Show entries** — dropdown (e.g. 25) controlling rows per page
- **Search** — text box, searches across table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right
- `Excel export icon` (green) — top right
- `Print icon` (green) — top right
- `Go` — applies filters and refreshes table
- `Sort arrows` — on sortable column headers

**Table columns:**

| Invoice No | Date | Buyer | Broker | City | Taxable | SGST | CGST | IGST | Total Tax | Discount | Rate Diff | Return Goods | Net Amount | Received | Voucher No | Voucher Date | Bank Name | Cheque Date | Cheque No |
| ---------- | ---- | ----- | ------ | ---- | ------- | ---- | ---- | ---- | --------- | -------- | --------- | ------------ | ---------- | -------- | ---------- | ------------ | --------- | ----------- | --------- |

**Grouping rows:** When a grouping tab is active (e.g. Broker Party), the table inserts subtotal header rows per broker and per party (e.g. "NO BROKER NAME", "SHRI SAI TRADERS", "VIMAL TRADING CO") showing aggregated Taxable, SGST, CGST, IGST, Discount, Rate Diff, Return Goods, Net Amount, and Received for that group before listing individual invoice line items underneath. Other groupings (Party Broker, Broker City, City Broker) return empty result sets in this dataset (table shows a "Processing..." state with no rows).

### 7.7 Interest Ledger

**Purpose:** Calculates interest on a party's outstanding balance over a date range, using configurable debit/credit interest rates and optional grace periods, showing total balance, interest, and total-with-interest.

**Navigation:** Home / Accounting / Interest Ledger

**Fields:**

- **Select Party** — dropdown (e.g. Bagreeji Smart Products)
- **Start Date** — date picker (e.g. 01-04-2023)
- **End Date** — date picker (e.g. 31-03-2024)
- **Dr %** — number input, debit interest rate
- **Cr %** — number input, credit interest rate
- **Enter Days** — number input, grace/calculation days
- **Gp Dr** — text input, grace period for debit
- **Gp Cr** — text input, grace period for credit

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Print icon` — top right
- `Export icon` — top right
- `GO` — applies filters and calculates interest
- `Print` — below table, prints report
- `Excel` — below table, exports report

**Table columns:**

| Name | Balance |
| ---- | ------- |

**Rows:** Total, Interest, Total With Interest

### 7.8 Rate Send

**Purpose:** Bulk-uploads rates via file import and sends rate information to parties via email, with a party selection list (2,101 parties) supporting search and multi-select.

**Navigation:** Home / Master / Rate Sent

**Fields:**

- **Choose file** — file upload input, no file chosen by default
- **Show entries** — dropdown (e.g. 100) controlling rows per page (upload-results table)
- **Search** — text box (upload-results table)
- **Select All** — checkbox, selects all parties in the list below
- **Search** — text box (party list table)

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right
- `Choose file` — opens file picker for rate upload
- `Send Email` — sends rate info to selected parties
- `Previous` / `Next` — pagination (upload-results table)
- Sort arrows — on Party Name, Email, Mobile columns (party list table)
- Per-row checkbox — Select column, selects individual party

**Table columns (upload results):**

| #   | Name | Select |
| --- | ---- | ------ |

**Table columns (party list):**

| SR  | Party Name | Email | Mobile | Select |
| --- | ---------- | ----- | ------ | ------ |

### 7.9 Party Balance

**Purpose:** Lists all parties with registration, address, and balance details — opening/closing credit and debit balances per party — with per-column inline filters, sorting, search, and pagination (2,127 entries).

**Navigation:** Home / Master / View Party Broker (sidebar label: Party Balance)

**Fields:**

- **Select Some Options** — multi-select dropdown, top of page, filters party list
- **Show entries** — dropdown (e.g. 25) controlling rows per page
- **Per-column filter inputs** — text boxes under each header (Name, Group, Registration Date, Address, City, State, Contact Person, Type, Opening Credit, Opening Debit, Type)

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Go` — applies top filter and refreshes table
- `Gear/settings icon` — top right
- `Print icon` (green) — top right
- `Excel export icon` (green) — top right
- `PDF export icon` (green) — top right
- Sort arrows — on Name, City sortable columns
- `Previous` / page numbers / `Next` — pagination

**Table columns:**

| SR  | Name | Group | Registration Date | Address | City | State | Contact Person | Type | Opening Credit | Opening Debit | Credit Balance | Debit Balance | Closing Credit | Closing Debit | Type |
| --- | ---- | ----- | ----------------- | ------- | ---- | ----- | -------------- | ---- | -------------- | ------------- | -------------- | ------------- | -------------- | ------------- | ---- |

### 7.10 TCS/TDS Party

**Purpose:** Shows party-wise TCS/TDS applicability data (Taka, Meter, Net Meter, Taxable Value, Invoice Value) for Purchase/Sales TCS/TDS, with a mode toggle and per-row action checkbox, likely to mark/include parties for TCS/TDS calculation.

**Navigation:** Home / Reports / Purchase TCS Party

**Fields:**

- **Mode toggle** — radio buttons: Purchase TDS Party, Purchase TCS Party, Sales TCS Party, Sales TDS Party
- **Select** — dropdown, filter (unspecified options)
- **All** — dropdown (first), filter
- **All** — dropdown (second), filter
- **Date range** — from date, to date (e.g. 01-04-2023 to 31-03-2024)
- **Show entries** — dropdown (e.g. 100) controlling rows per page
- **Per-column filter inputs** — text boxes under Supplier Name, Taka, Meter, Net Meter, Taxable Value headers

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right
- `GO` — applies filters and refreshes table
- `Print icon` (green) — top right
- `Excel export icon` (green) — top right
- `Print` — above table, secondary print trigger
- Sort arrow — on Supplier Name column
- Per-row checkbox — Action column, includes/excludes party
- `Previous` / page numbers / `Next` — pagination

**Table columns:**

| Supplier Name | Taka | Meter | Net Meter | Taxable Value | Invoice Value | Action |
| ------------- | ---- | ----- | --------- | ------------- | ------------- | ------ |

**Bottom row:** Total row (sums Taka, Meter, Net Meter, Taxable Value, Invoice Value)

### 7.11 TCS Matrix

**Purpose:** Shows a broker-wise matrix of TCS grand totals for a selected voucher type — currently showing no data.

**Navigation:** Home / Accounting / Matrix

**Fields:**

- **Voucher type** — dropdown (e.g. Reciept Voucher)
- **Show entries** — dropdown (e.g. 25) controlling rows per page
- **Search** — text box, searches across table

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right
- `Go` — applies filter and refreshes table
- `Excel` — exports table
- `PDF` — exports table
- `Print` — prints table
- Sort arrows — on Name, Broker columns
- `Previous` / `Next` — pagination

**Table columns:**

| SR  | Name | Broker | Grand Total |
| --- | ---- | ------ | ----------- |

**Bottom row:** Total row

## 8. Tax

### 8.1 GST Summary

**Purpose:** Shows a GST liability summary for a selected branch/GSTIN and date range, broken into Sales, Sales Return, Purchase, and Purchase Return sections with taxable value and CGST/SGST/IGST breakup, culminating in GSTR-1 and GSTR-2 form totals.

**Navigation:** Home / Tax / GST

**Fields:**

- **Branch/GSTIN** — multi-select tag input (e.g. "BHAGAL BRANCH - 24AANFD1775C1ZM"), removable tag
- **Date range** — from date, to date (e.g. 01-09-2024 to 30-09-2024)

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Export icon` (blue) — next to branch selector
- `Gear/settings icon` — top right
- `GO` — applies filters and refreshes table
- `Print` — top right
- `Excel` — top right
- Row-level icons (blue) — per detail row (e.g. B2B, B2CL, B2CS, EXEMP, B2BUR, IMP_G, IMP_S), likely drill-down/export per line

**Table columns:**

| Detail | Taxable | CGST | SGST | IGST | Total | Liability |
| ------ | ------- | ---- | ---- | ---- | ----- | --------- |

**Rows (Sales section - A):** B2B, B2CL, B2CS, EXEMP, Sales Total; Sales Return sub-section with CDNR (Sales Return, Sales Creditnote, Sales Debitnote) and CDNUR (Sales Return, Sales Creditnote, Sales Debitnote), Sales Return Total, GSTR-1 Form

**Rows (Purchase section):** B2B, B2BUR, IMP_G, IMP_S, EXEMP, Purchase Total; Purchase Return sub-section with CDNR (Purchase Return, Purchase Debitnote, Purchase Creditnote) and CDNUR (Purchase Return, Purchase Debitnote, Purchase Creditnote), Purchase Return Total, GSTR-2 Form

### 8.2 Form GSTR1

**Purpose:** Prepares and displays GSTR-1 return data by section (B2B, B2CL, B2CS, CDNR, CDNUR, EXP, AT, ATADJ, EXEMP, HSN, DOCS, and amendment variants), for a selected branch/GSTIN and date range, with GSTN verification and multi-format export.

**Navigation:** Home / Tax / GSTR1

**Fields:**

- **Section toggle (primary)** — radio buttons: B2B, B2CL, B2CS, CDNR, CDNUR, EXP, AT, ATADJ, EXEMP, HSN, DOCS
- **Section toggle (amendment)** — radio buttons: b2ba, b2cla, b2csa, cdnra, cdnura, expa, ata, atadj
- **Branch/GSTIN** — multi-select tag input (e.g. "BHAGAL BRANCH - 24AANFD1775C1ZM"), removable tag
- **Date range** — from date, to date (e.g. 01-09-2023 to 30-09-2023)

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Verify with GSTN` — top right, validates data against GSTN portal
- `Gear/settings icon` — top right
- `Print icon` — below section toggles
- `File/document icon` — below section toggles
- `Email icon` — below section toggles
- `Export icons` (multiple colored, 5x) — below section toggles, likely different export formats (Excel, JSON, etc.)
- `GO` — applies filters and refreshes table

**Table columns (summary row):**

| (blank) | (blank) | Rate | Total Taxable Value | Total Cess | (blank) | Book |
| ------- | ------- | ---- | ------------------- | ---------- | ------- | ---- |

**Table columns (detail rows):**

| Type | Invoice No | Place of Supply | Rate | Taxable Value | Cess Amount | E-Commerce GSTN | Book |
| ---- | ---------- | --------------- | ---- | ------------- | ----------- | --------------- | ---- |

### 8.3 GSTR2

**Purpose:** Prepares and displays GSTR-2 (purchase-side) return data by section (B2B, B2BUR, IMP_G, IMP_S, CDNR, CDNUR, AT, ATADJ, EXEMP, ITCR, HSNSUM), showing ITC availed and eligibility per invoice, for a selected branch/GSTIN and date range, with GSTN format export.

**Navigation:** Home / Tax / GSTR2

**Fields:**

- **Section toggle** — radio buttons: B2B, B2BUR, IMP_G, IMP_S, CDNR, CDNUR, AT, ATADJ, EXEMP, ITCR, HSNSUM
- **Branch/GSTIN** — multi-select tag input (e.g. "BHAGAL BRANCH - 24AANFD1775C1ZM"), removable tag
- **Date range** — from date, to date (e.g. 01-09-2023 to 30-09-2023)

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right
- `Print icon` — below section toggles
- `GSTN Format` (green) — exports in GSTN format
- `GSTN V1.1 (test)` (orange) — exports in GSTN V1.1 test format
- `GO` — applies filters and refreshes table
- `Book` — per-row action, marks invoice as booked
- `Action` — per-row action, additional row action

**Table columns (summary row):**

| No of Recipients | No of Invoice | (blank) | Total Inv Value | (blank) | (blank) | (blank) | Total Taxable Value | IGST Total | CGST Total | SGST Total | Total Cess | (blank) | (blank) | (blank) | (blank) | (blank) | Book | Action |
| ---------------- | ------------- | ------- | --------------- | ------- | ------- | ------- | ------------------- | ---------- | ---------- | ---------- | ---------- | ------- | ------- | ------- | ------- | ------- | ---- | ------ |

**Table columns (detail rows):**

| GSTIN of Supplier | Invoice Number | Invoice Date | Invoice Value | Place of Supply | Reverse Charge | Invoice Type | Rate | Taxable Value | Integrated Tax | Central Tax | State or UT Tax | Cess | Eligibility for ITC | Availed ITC Integrated Tax | Availed ITC Central Tax | Availed ITC State/UT Tax | Availed ITC Cess | Book | Action |
| ----------------- | -------------- | ------------ | ------------- | --------------- | -------------- | ------------ | ---- | ------------- | -------------- | ----------- | --------------- | ---- | ------------------- | -------------------------- | ----------------------- | ------------------------ | ---------------- | ---- | ------ |

### 8.4 GSTR2 Reco

**Purpose:** Reconciles purchase register data (PWP) against GSTN 2A data — uploading 2A JSON, viewing summary counts/differences, generating supplier-wise reports, and matching/reviewing individual invoices (Purchase and CDNR) with tax and value differences.

**Navigation:** Home / Master / GSTR2 RECO

**Fields:**

- **Date range** — from date, to date (e.g. 01-09-2023 to 30-09-2023)
- **Tabs** — Prepare Reco, GSTN Wise Report, Match & Review
- **(Prepare Reco tab) Reconciliation date range** — from date, to date (used with Reconciliation button)
- **(Prepare Reco tab) Select Month of GSTR2 Excel** — dropdown/text input
- **(Match & Review tab) Sub-tabs** — Purchase, CDNR

**Buttons / Actions:**

- `Heart icon` — next to heading
- `Gear/settings icon` — top right
- `Go` — applies top date range filter
- **Prepare Reco tab:**
  - `2A Json` (orange) — uploads GSTN 2A JSON data
  - `Reconciliation` (blue) — runs reconciliation between GSTN and purchase data
  - `GSTR2 Excel` (orange) — exports/generates GSTR2 Excel for selected month
- **GSTN Wise Report tab:**
  - `Print` (green) — prints report
  - `Excel` (green) — exports report
  - `View All` — per supplier row, opens full detail
- **Match & Review tab:**
  - `Print` (green) — prints match/review data
  - `Excel` (green) — exports match/review data

**Table columns (Prepare Reco — Summary 2023-2024, left):**

| 2A  | (value) |
| --- | ------- |

**Table columns (Prepare Reco — Summary 2023-2024, right):**

| Month | B2B-2A | B2B-2 | CDNR-2A | CDNR-2 |
| ----- | ------ | ----- | ------- | ------ |

**Table columns (GSTN Wise Report):**

| Supplier Details | (sub-row label) | No of Docs | Docs Diff | Tax Value | Tax Difference | Taxable Value | Taxable Difference | Action |
| ---------------- | --------------- | ---------- | --------- | --------- | -------------- | ------------- | ------------------ | ------ |

**Rows:** All Supplier (with sub-rows PWP Data » and Suppier »)

**Table columns (Match & Review — Purchase/CDNR):**

| #   | Supplier (2A): Inv No, Inv Date, Taxable Value, Total Value, Tax Value | Tax Diff | PWP Data (Purchase Register): Inv No, Inv Date, Taxable Value, Total Value, Tax Value | Recon Status | Action |
| --- | ---------------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------- | ------------ | ------ |

### 8.5 GSTR3B

**Purpose:** Prepares and displays the GSTR-3B monthly summary return — outward supplies liable to tax, eligible ITC, exempt/nil-rated/non-GST inward supplies, interest & late fee payable, inter-state supplies to unregistered persons, and final tax payment/TDS-TCS credit — for a selected branch/GSTIN and date range.

**Navigation:** Home / Tax / GSTR3B

**Fields:**

- **Branch/GSTIN** — multi-select dropdown ("Select Some Options")
- **Date range** — from date, to date (e.g. 01-09-2023 to 30-09-2023)
- **All amount fields across sections** — editable/read-only currency inputs (₹), most defaulting to 0.00

**Buttons / Actions:**

- `Heart icon` — next to heading (not visible but consistent with pattern)
- `GO` — applies filters and refreshes form
- `GST Balance Matrix` (blue) — top right, opens balance matrix view
- `Print icon` — top right
- `Excel export icon` — top right
- `Jv Entry` (green) — within section 6.1, creates a journal voucher entry

**Section 3.1 — Details of Outward Supplies and inward supplies liable to reverse charge:**

| Nature of Supplies | Total Taxable Value (₹) | Integrated Tax (₹) | Central Tax (₹) | State/UT Tax (₹) | Cess (₹) |
| ------------------ | ----------------------- | ------------------ | --------------- | ---------------- | -------- |

**Rows:** (A) Outward Taxable Supplies (Other Than Zero Rated, Nil Rated And Exempted), (B) Outward Taxable Supplies (Zero Rated), (C) Other Outward Supplies (Nil Rated, Exempted), (D) Inward Supplies (Liable To Reverse Charge), (E) Non-GST Outward Supplies

**Section 4 — Eligible ITC:**

| Details | Integrated Tax (₹) | Central Tax (₹) | State/UT Tax (₹) | Cess (₹) |
| ------- | ------------------ | --------------- | ---------------- | -------- |

**Rows:** (A) ITC Available (Whether In Full Or Part) — (1) Import Of Goods, (2) Import Of Services, (3) Inward Supplies Liable To Reverse Charge (Other Than 1 & 2 Above), (4) Inward Supplies From ISD, (5) All Other ITC; (B) ITC Reversed — (1) As Per Rules 42 & 43 Of CGST Rules, (2) Other; (C) Net ITC Available (A) – (B); (D) Ineligible ITC — (1) As Per Section 17(5), (2) Others

**Section 5 — Values of exempt, nil-rated and non-GST inward supplies:**

| Nature of Supplies | Inter-State Supplies (₹) | Intra-State Supplies (₹) |
| ------------------ | ------------------------ | ------------------------ |

**Rows:** From A Supplier Under Composition Scheme, Exempt And Nil Rated Supply; Non GST Supply

**Section 5.1 — Interest & late fee payable:**

| Description | Integrated Tax | Central Tax | State/UT Tax | Cess |
| ----------- | -------------- | ----------- | ------------ | ---- |

**Rows:** Interest

**Section 3.2 — Of the supplies shown in 3.1(a), details of inter-state supplies made to unregistered persons, composition taxable person and UIN holders:**

| Place of Supply (State/UT) | Total Taxable Value (₹) | Amount of Integrated Tax (₹) |
| -------------------------- | ----------------------- | ---------------------------- |

**Section 6.1 — Payment of Tax:**

| Description | Tax Payable | Paid Through ITC (Integrated Tax, Central Tax, State/UT Tax, Cess) | Tax Paid TDS/TCS | Tax/Cess Paid In Cash | Interest | Late Fee |
| ----------- | ----------- | ------------------------------------------------------------------ | ---------------- | --------------------- | -------- | -------- |

**Rows:** Integrated Tax, Central Tax, State/UT, Cess, Total

**Section 6.2 — TDS/TCS Credit:**

| Details | Integrated Tax | Central Tax | State/UT Tax |
| ------- | -------------- | ----------- | ------------ |

**Rows:** TDS, TCS
