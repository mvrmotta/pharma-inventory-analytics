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

  dim_item {
    int item_id PK
    text sku UK
    text description
    text unit
    text category
    text abc_class  "A/B/C"
    text criticality "High/Medium/Low"
    int shelf_life_days
    text manufacturer
    numeric(12,2) avg_unit_cost
  }

  dim_supplier {
    int supplier_id PK
    text name
    text tax_id
    int lead_time_days
    int min_lot
  }

  dim_location {
    int location_id PK
    text name
    text city
  }

  dim_calendar {
    date date PK
    int year
    int month
    int week
    boolean is_holiday
    boolean is_weekend
  }

  f_consumption {
    bigserial id PK
    date date FK
    int item_id FK
    int location_id FK
    numeric(12,3) qty
    text demand_source
  }

  f_purchase_order {
    bigserial po_id PK
    date order_date FK
    int item_id FK
    int supplier_id FK
    int location_id FK
    numeric(12,3) qty
    numeric(12,2) unit_price
    date promised_date
    text status
  }

  f_receipt {
    bigserial receipt_id PK
    date receipt_date FK
    bigint po_id FK
    int item_id FK
    int supplier_id FK
    int location_id FK
    numeric(12,3) qty
    numeric(12,2) unit_price
  }

  f_inventory_daily {
    bigserial id PK
    date date FK
    int item_id FK
    int location_id FK
    numeric(12,3) qty
    numeric(12,2) value
  }

  f_lot_expiry {
    bigserial id PK
    int item_id FK
    int location_id FK
    text lot_code
    date expiry_date
    numeric(12,3) lot_qty
  }
