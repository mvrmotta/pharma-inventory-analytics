# Data Model Documentation

## Purpose
This document describes the conceptual and logical data model for the *Pharmaceutical Inventory Optimization Project*. It defines key entities, their business purpose, and the relationships required to support stock visibility, forecasting, and decision-making.

---

## Entity-Relationship Diagram (ERD)

```mermaid
erDiagram
  dim_item ||--o{ f_consumption : "item_id"
  dim_item ||--o{ f_purchase_order : "item_id"
  dim_item ||--o{ f_receipt : "item_id"
  dim_item ||--o{ f_inventory_daily : "item_id"
  dim_item ||--o{ f_lot_expiry : "item_id"

  dim_supplier ||--o{ f_purchase_order : "supplier_id"
  dim_supplier ||--o{ f_receipt : "supplier_id"

  dim_location ||--o{ f_consumption : "location_id"
  dim_location ||--o{ f_purchase_order : "location_id"
  dim_location ||--o{ f_receipt : "location_id"
  dim_location ||--o{ f_inventory_daily : "location_id"
  dim_location ||--o{ f_lot_expiry : "location_id"

  dim_calendar ||--o{ f_consumption : "date"
  dim_calendar ||--o{ f_purchase_order : "order_date"
  dim_calendar ||--o{ f_receipt : "receipt_date"
  dim_calendar ||--o{ f_inventory_daily : "date"


## Entity Definitions

This section describes the purpose and business meaning behind each table in the data model.  
It helps analysts and stakeholders understand how data flows through the pharmaceutical inventory process.

---

### 📌 `dim_item` — Product Master Data
Represents all pharmaceutical products and medical consumables managed in inventory.

| Attribute | Meaning |
|---|---|
| SKU | Unique item identifier used in operations |
| Description | Product name displayed to users |
| Unit | Measurement unit (unit, bottle, pack, ml…) |
| Category | Logical grouping (Antibiotic, Analgesic, PPE…) |
| ABC Class | Value-based importance (A = high value impact) |
| Criticality | Operational risk if the item runs out |
| Shelf Life (days) | Validity period before expiration |
| Manufacturer | Company that produces the item |
| Avg Unit Cost | Standard average cost used for inventory valuation |

✅ Key business impact: inventory valuation, risk exposure, demand classification.

---

### 🏭 `dim_supplier` — Supplier Information
Describes vendors and how they supply the organization.

| Attribute | Meaning |
|---|---|
| Name | Supplier branding used for reporting |
| Tax ID | Legal company document identifier |
| Lead Time | Expected delivery delay in days |
| Minimum Lot | Minimum order quantity per purchase |

✅ Supports forecasting reorder points and procurement planning.

---

### 🧱 `dim_location` — Inventory Storage / Usage Sites
Tracks where stock physically exists or gets consumed.

| Attribute | Meaning |
|---|---|
| Name | Storage location or pharmacy name |
| City | Location context for logistics decisions |

✅ Enables multi-site analytics and operational scaling.

---

### 📆 `dim_calendar` — Time Intelligence Table
Centralized reference for date-related filtering and time-series analysis.

| Attribute | Meaning |
|---|---|
| Date | Primary key (each row is 1 day) |
| Year, Month, Week | Used for aggregation and reporting |
| Weekend, Holiday | Seasonality impact tracking |

✅ Powers DOH, turnover, and consumption seasonality analytics.

---

### 📥 `f_receipt` — Goods Received from Suppliers
Tracks inbound flow of inventory.

| Attribute | Meaning |
|---|---|
| Receipt Date | Day items arrived and became available |
| PO Reference | Links to ordered quantity and lead time measurement |
| Qty Received | Actual quantity added into stock |
| Unit Price | Real cost from supplier |

✅ Validates supplier delivery performance and cost accuracy.

---

### 🧪 `f_consumption` — Items Used in Operations
Represents outbound movements that reduce inventory.

| Attribute | Meaning |
|---|---|
| Date | When the item was consumed |
| Demand Source | Optional context (prescription, procedure, etc.) |
| Qty Consumed | Quantity subtracted from stock |

✅ Enables forecasting and stockout detection.

---

### 📦 `f_inventory_daily` — End-of-Day Inventory Snapshot
Frozen records of stock after all receipts/consumption each day.

| Attribute | Meaning |
|---|---|
| Qty On Hand | Current inventory available |
| Value On Hand | Qty × Avg Unit Cost |

✅ Core metric for DOH, turnover, and financial exposure.

---

### ⛔ `f_lot_expiry` — Expiration Control per Lot
Tracks shelf-life risk for pharmaceutical safety.

| Attribute | Meaning |
|---|---|
| Expiry Date | Legal cutoff for usage |
| Lot Code | Helps prevent traceability issues |
| Lot Qty | Amount expiring under this batch |

✅ Ensures compliance and minimizes inventory waste.

---

🎯 In summary:  
- **dim\_*** tables tell us *what, who, where, and when*  
- **f\_*** tables tell us *how much enters or leaves stock over time*  
