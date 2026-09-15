# Dhanhar Masala Application Documentation

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
