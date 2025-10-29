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
