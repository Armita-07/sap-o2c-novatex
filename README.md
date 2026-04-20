# 🏭 NovaTex Industries - SAP Order-to-Cash (O2C) Capstone Project

**Student:** Armita Patro
**Roll Number:** 23051737 
**Batch/Program:** SAP BTP DEVELOPER | KIIT  DU
**Submission Date:** April 21, 2026  

---

## 📌 Project Overview

This capstone project demonstrates an **end-to-end Order-to-Cash (O2C) cycle** implemented in SAP SD (Sales & Distribution) for a fictitious company - **NovaTex Industries Pvt. Ltd.**, a mid-sized textile manufacturing and distribution enterprise headquartered in Bhubaneswar, Odisha.

The O2C cycle covers the complete journey from a customer placing an order to the company receiving payment - including sales order creation, delivery processing, goods issue, billing, and accounts receivable posting.

---

## 🏢 Company Profile — NovaTex Industries Pvt. Ltd.

| Parameter | Details |
|-----------|---------|
| Company Code | NTX1 |
| Company Name | NovaTex Industries Pvt. Ltd. |
| Industry | Textile Manufacturing & Distribution |
| HQ | Bhubaneswar, Odisha, India |
| Currency | INR (Indian Rupee) |
| Fiscal Year | April – March |
| Sales Org | NTX_SO (NovaTex Sales Org) |
| Distribution Channel | 10 – Wholesale |
| Division | 01 – Textiles |

---

## 🔄 O2C Process Flow

```
Customer Inquiry (VA11)
        ↓
Quotation (VA21)
        ↓
Sales Order (VA01)
        ↓
Delivery Creation (VL01N)
        ↓
Goods Issue (VL02N)
        ↓
Billing/Invoice (VF01)
        ↓
Accounting Entry (FI Integration)
        ↓
Payment Receipt (F-28)
```

---

## 📁 Repository Structure

```
sap-o2c-novatex/
│
├── README.md                          ← This file
│
├── docs/
│   ├── Project_Documentation.pdf      ← Main 5-page project report
│   ├── O2C_Process_Steps.md           ← Step-by-step SAP configuration guide
│   └── Company_Blueprint.md           ← NovaTex org structure & setup
│
├── screenshots/
│   ├── 01_customer_master.png         ← Customer master record (XD01)
│   ├── 02_material_master.png         ← Material master (MM01)
│   ├── 03_sales_order.png             ← Sales order creation (VA01)
│   ├── 04_delivery.png                ← Outbound delivery (VL01N)
│   ├── 05_goods_issue.png             ← Post goods issue (VL02N)
│   ├── 06_billing.png                 ← Billing document (VF01)
│   └── 07_accounting_entry.png        ← FI posting (FB03)
│
├── config/
│   ├── enterprise_structure.md        ← SAP enterprise structure config
│   ├── pricing_procedure.md           ← Pricing condition setup (RVAA01)
│   └── output_determination.md        ← Invoice output config
│
└── test_data/
    ├── customer_master_data.csv        ← Sample customer records
    └── material_master_data.csv        ← Sample material records
```

---

## ⚙️ SAP Configuration Summary

### Enterprise Structure
- **Company Code:** NTX1
- **Sales Organization:** NTX_SO → Assigned to NTX1
- **Distribution Channel:** 10 (Wholesale)
- **Division:** 01 (Textiles)
- **Sales Area:** NTX_SO / 10 / 01

### Key Master Data
- **Customer Master:** Fabric Bazaar Ltd. (Customer No: 100001)
- **Material Master:** Premium Cotton Fabric Roll (Mat No: MAT-CTN-001)
- **Pricing:** Base Price + GST 12% + Freight = Net Value

### Document Flow (Sample Transaction)
| Step | T-Code | Document No |
|------|--------|-------------|
| Sales Order | VA01 | 0000012345 |
| Delivery | VL01N | 0080001234 |
| Goods Issue | VL02N | 0080001234 |
| Invoice | VF01 | 0090001234 |
| Accounting | FB03 | 1400001234 |

## Tech Stack used

Technology | PurposeSAP 
|----------|-----------|
| S/4HANACore | ERP platform for O2C execution |
| SAP SD (Sales & Distribution) | Sales order, delivery, billing |
| SAP MM (Materials Management) | Inventory & goods issue |
| SAP FI (Financial Accounting) | Accounting entries, AR, payment |
| SAP Fiori | Modern UI layer for SAP transactions |
| SAP Condition Technique | Pricing procedure configuration |
|SPRO (IMG) | Enterprise structure customization |
| Markdown | Documentation & README |
| GitHub | Version control & project hosting |

## 🎯 Key Learning Outcomes

1. Understanding SAP SD enterprise structure configuration
2. End-to-end O2C process execution in SAP
3. Integration touchpoints between SD, MM, and FI modules
4. Pricing procedure and condition technique in SAP
5. Output determination and document management

---

## 🚀 Future Improvements

- Implement credit management and credit check at sales order stage
- Configure returns and complaints process (RE document type)
- Add intercompany sales scenario
- Integrate with SAP CRM for customer interaction history

---

## 📄 Documentation

Full project documentation is available in [`docs/Project_Documentation.pdf`](docs/Project_Documentation.pdf)

---

*This project is submitted as part of the SAP BTP DEVELOPER PROJECT at KIIT DU. All company data is fictitious and created for educational purposes.* 

Submitted by :
Name- Armita Patro
ROLL NO- 23051737
SAP BTP DEVELOPER
