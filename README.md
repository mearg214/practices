# practices
```mermaid
erDiagram
    USER {
        SERIAL user_id PK
        VARCHAR full_name
        VARCHAR email
        TEXT password_hash
        TIMESTAMP created_at
    }

    SHIPPING_INFO {
        SERIAL shipping_id PK
        INT user_id FK
        TEXT address
        VARCHAR city
        VARCHAR postal_code
        VARCHAR country
    }

    CATEGORY {
        SERIAL category_id PK
        VARCHAR category_name
    }

    ITEM {
        SERIAL item_id PK
        INT seller_id FK
        INT category_id FK
        VARCHAR name
        VARCHAR brand
        VARCHAR condition
        NUMERIC price
        TIMESTAMP created_at
    }

    GADGET {
        INT item_id PK, FK
        VARCHAR model
        TEXT specs
        INT storage_gb
        INT ram_gb
    }

    ACCESSORY {
        INT item_id PK, FK
        VARCHAR accessory_type
        VARCHAR compatibility
    }

    INVENTORY {
        INT item_id PK, FK
        INT quantity
        VARCHAR status
    }

    ORDER {
        SERIAL order_id PK
        INT buyer_id FK
        TIMESTAMP order_date
        NUMERIC total_amount
    }

    ORDER_ITEM {
        SERIAL order_item_id PK
        INT order_id FK
        INT item_id FK
        NUMERIC price_at_purchase
    }

    USER ||--o{ SHIPPING_INFO : has
    USER ||--o{ ITEM : sells
    CATEGORY ||--o{ ITEM : categorizes

    ITEM ||--|| INVENTORY : tracked_by

    ITEM ||--o| GADGET : "is a"
    ITEM ||--o| ACCESSORY : "is a"

    USER ||--o{ ORDER : places
    ORDER ||--o{ ORDER_ITEM : contains
    ITEM ||--o{ ORDER_ITEM : included_in