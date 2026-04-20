# SAP Order-to-Cash (O2C) — Step-by-Step Process Guide
## NovaTex Industries Pvt. Ltd. | SAP SD Capstone

---

## PHASE 1: ENTERPRISE STRUCTURE SETUP

### Step 1.1 — Define Company Code (T-Code: OX02)
**Menu Path:** SPRO → Enterprise Structure → Definition → Financial Accounting → Define Company Code

| Field | Value |
|-------|-------|
| Company Code | NTX1 |
| Company Name | NovaTex Industries Pvt. Ltd. |
| City | Bhubaneswar |
| Country | IN |
| Currency | INR |
| Language | EN |

### Step 1.2 — Define Sales Organization (T-Code: OVX5)
**Menu Path:** SPRO → Enterprise Structure → Definition → Sales & Distribution → Define Sales Organization

| Field | Value |
|-------|-------|
| Sales Org | NTX_SO |
| Description | NovaTex Sales Organization |
| Company Code | NTX1 |

### Step 1.3 — Define Distribution Channel (T-Code: OVXI)
| DC Code | Description |
|---------|-------------|
| 10 | Wholesale |
| 20 | Retail |

### Step 1.4 — Define Division (T-Code: OVX3)
| Division | Description |
|----------|-------------|
| 01 | Textiles |
| 02 | Accessories |

### Step 1.5 — Assignments
1. Assign Sales Org to Company Code: NTX_SO → NTX1
2. Assign Distribution Channel to Sales Org: 10 → NTX_SO
3. Assign Division to Sales Org: 01 → NTX_SO
4. Set up Sales Area: NTX_SO / 10 / 01

---

## PHASE 2: MASTER DATA CREATION

### Step 2.1 — Customer Master (T-Code: XD01)
**Account Group:** 0001 (Sold-to Party)

| Tab | Field | Value |
|-----|-------|-------|
| General | Name | Fabric Bazaar Ltd. |
| General | Search Term | FABAZ |
| General | Street | 12 Commerce Street |
| General | City | Cuttack |
| General | Country | IN |
| General | Region | OD |
| Company Code | Rec. Account | 140000 |
| Company Code | Payment Terms | ZN30 (Net 30 days) |
| Sales Area | Sales District | OD001 |
| Sales Area | Customer Group | 01 |
| Sales Area | Delivery Priority | 02 (Normal) |
| Sales Area | Shipping Conditions | 01 (Standard) |
| Sales Area | Incoterms | CIF – Cuttack |

**Partner Functions:**
- SP (Sold-to): 100001 – Fabric Bazaar Ltd.
- SH (Ship-to): 100001
- BP (Bill-to): 100001
- PY (Payer): 100001

### Step 2.2 — Material Master (T-Code: MM01)
**Industry Sector:** M (Mechanical)  
**Material Type:** FERT (Finished Product)

| View | Field | Value |
|------|-------|-------|
| Basic Data 1 | Material | MAT-CTN-001 |
| Basic Data 1 | Description | Premium Cotton Fabric Roll |
| Basic Data 1 | Base UoM | ROL (Roll) |
| Basic Data 1 | Material Group | 001 |
| Sales Org 1 | Division | 01 |
| Sales Org 1 | Tax Category | MWST |
| Sales Org 2 | Item Category Group | NORM |
| MRP 1 | MRP Type | PD |
| Accounting 1 | Price Control | S (Standard) |
| Accounting 1 | Standard Price | 5,000 INR |

### Step 2.3 — Pricing Condition Records (T-Code: VK11)
**Condition Type: PR00 (Base Price)**

| Condition | Sales Org | DC | Customer | Material | Amount |
|-----------|-----------|-----|----------|----------|--------|
| PR00 | NTX_SO | 10 | 100001 | MAT-CTN-001 | 5,500 INR |

**Tax Condition: MWST (GST 12%)**  
Maintained in FI Tax configuration — automatically calculated.

---

## PHASE 3: ORDER-TO-CASH CYCLE EXECUTION

### Step 3.1 — Customer Inquiry (T-Code: VA11) [Optional]
1. Execute VA11
2. Enter Inquiry Type: IN
3. Sales Area: NTX_SO / 10 / 01
4. Sold-to Party: 100001
5. Add line item: MAT-CTN-001, Qty: 100 ROL
6. Requested Delivery Date: 05.05.2026
7. Save → Inquiry No generated: 0000000001

### Step 3.2 — Quotation (T-Code: VA21) [Optional]
1. Execute VA21
2. Quotation Type: QT
3. Reference Inquiry: 0000000001
4. Review pricing, adjust if needed
5. Validity: 01.04.2026 to 30.04.2026
6. Save → Quotation No: 0000020001

### Step 3.3 — Sales Order Creation (T-Code: VA01) ⭐ CORE STEP
1. Execute VA01
2. Order Type: **OR** (Standard Order)
3. Sales Area: NTX_SO / 10 / 01
4. Click Enter
5. **Header Data:**
   - Sold-to Party: 100001 (Fabric Bazaar Ltd.)
   - PO Number: PO-FAB-2026-001
   - PO Date: 01.04.2026
   - Requested Delivery Date: 05.05.2026
6. **Item Overview:**
   - Material: MAT-CTN-001
   - Order Qty: 100 ROL
7. **Pricing Tab (Conditions):**
   - PR00: 5,500 × 100 = 5,50,000 INR
   - MWST (GST 12%): 66,000 INR
   - Net Value: 6,16,000 INR
8. Check Item Category: **TAN** (Standard Item)
9. Schedule Line Category: **CP** (Planned Order)
10. Save → **Sales Order No: 0000012345**

### Step 3.4 — Delivery Creation (T-Code: VL01N) ⭐ CORE STEP
1. Execute VL01N
2. Shipping Point: NTX_SP
3. Selection Date: 05.05.2026
4. Sales Order: 0000012345
5. Click Enter — system copies line items
6. **Delivery Qty:** 100 ROL (confirm full delivery)
7. **Picking Tab:**
   - Enter Storage Location: 0001
   - Picked Qty: 100
8. Save → **Delivery No: 0080001234**

### Step 3.5 — Post Goods Issue (T-Code: VL02N) ⭐ CORE STEP
1. Execute VL02N
2. Delivery No: 0080001234
3. Verify Goods Movement Type: **601** (GI for Delivery)
4. Click **Post Goods Issue**
5. System Posts:
   - Inventory reduced by 100 ROL
   - COGS debited: 5,00,000 INR
   - Inventory account credited: 5,00,000 INR
6. **Material Document: 4900001234**
7. Delivery status changes to: **C (Completed)**

### Step 3.6 — Billing / Invoice Creation (T-Code: VF01) ⭐ CORE STEP
1. Execute VF01
2. Billing Type: **F2** (Invoice)
3. Delivery Document: 0080001234
4. Click Execute
5. Verify billing items and pricing
6. Check Output Type: **RD00** (Invoice Print)
7. Save → **Billing Document No: 0090001234**
8. **Accounting Entry Auto-Posted:**
   - Dr. Customer (140000): 6,16,000 INR
   - Cr. Revenue (500000): 5,50,000 INR
   - Cr. GST Payable (175000): 66,000 INR

### Step 3.7 — View Accounting Document (T-Code: FB03)
1. Execute FB03
2. Document No: 1400001234
3. Company Code: NTX1
4. Fiscal Year: 2026
5. Verify debit/credit entries match billing document

### Step 3.8 — Customer Payment Receipt (T-Code: F-28)
1. Execute F-28
2. Document Date: 30.04.2026
3. Company Code: NTX1
4. Currency: INR
5. Account: Bank Account (113000)
6. Amount: 6,16,000 INR
7. Open Item Selection:
   - Account: 100001 (Fabric Bazaar Ltd.)
   - Select billing document 0090001234
8. Post → **Clearing Document: 1500001234**
9. Customer open item cleared to ZERO

---

## PHASE 4: VERIFICATION & REPORTING

### Step 4.1 — Document Flow Check (T-Code: VA03)
1. Open Sales Order 0000012345
2. Click Environment → Document Flow
3. Verify complete chain:
   - Sales Order ✓
   - Delivery ✓
   - Goods Issue ✓
   - Invoice ✓
   - Accounting Document ✓
   - Clearing Document ✓

### Step 4.2 — Sales Reports
- **VA05** — List of Sales Orders
- **VF05** — List of Billing Documents
- **FBL5N** — Customer Line Items (AR)

---

## INTEGRATION SUMMARY

| Module | Touch Point | T-Code |
|--------|------------|--------|
| SD ↔ MM | Goods Issue reduces stock | VL02N |
| SD ↔ FI | Billing creates accounting document | VF01 |
| SD ↔ CO | Revenue posted to CO-PA | Automatic |
| FI ↔ Bank | Payment clears AR open items | F-28 |

---

*Document prepared for KIIT SAP Capstone Project — NovaTex Industries O2C Scenario*
