```mermaid
erDiagram

    USER {
        int user_id PK
        string first_name
        string last_name
        string email UK
        string role
        boolean is_active
        datetime create
    }

    PASSWORD {
        int user_id PK, FK
        string password_hash
        datetime created_at
        datetime updated_at
    }

    PRODUCT {
        int product_id PK
        string name
        string barcode UK
        decimal unit_price
        int quantity_at_hand
        int reorder_level
        int reorder_quantity
        int safety_stock
        int category_id FK
        int supplier_id FK
    }

    SUPPLIER {
        int supplier_id PK
        string name
        string phone
        string address
    }

    CATEGORY {
        int category_id PK
        string name UK
        string description
    }

    PURCHASE {
        int purchase_id PK
        int supplier_id FK
        int user_id FK
        date purchase_date
        decimal total_cost
        string status
        date expected_date
    }

    PURCHASE_ITEM {
        int purchase_item_id PK
        int purchase_id FK
        int product_id FK
        int quantity
        decimal unit_price
    }

    SALE {
        int sale_id PK
        int user_id FK
        datetime sale_date
        decimal total_amount
    }

    SALE_ITEM {
        int sale_item_id PK
        int sale_id FK
        int product_id FK
        int quantity
        decimal unit_price
    }

    RESTOCK_RECOMMENDATION {
      string recommendation_id PK 
      int product_id FK 
      int purchase_id FK "nullable"
      datetime generated_at 
      decimal avg_daily_demand
      int lead_time_days
      int safety_stock
      int reorder_point
      int quantity_on_hand
      int quantity_on_order
      int recommended_quantity
      string explanation
      string status
    }

    USER ||--|| PASSWORD : has

    USER ||--o{ PURCHASE : records
    USER ||--o{ SALE : processes

    SUPPLIER ||--o{ PURCHASE : supplies
    SUPPLIER ||--o{ PRODUCT : provides

    CATEGORY ||--o{ PRODUCT : groups

    PURCHASE ||--|{ PURCHASE_ITEM : contains
    PURCHASE |o--o{ RESTOCK_RECOMMENDATION: fullfils

    PRODUCT ||--o{ PURCHASE_ITEM : appears_in

    SALE ||--|{ SALE_ITEM : contains

    PRODUCT ||--o{ SALE_ITEM : appears_in
    PRODUCT ||--o{ RESTOCK_RECOMMENDATION: gets

```


### Relationship
Supplier -> Product	(one-to-many)	A supplier provides many products, and each product has one default supplier.

Supplier -> Purchase	(one-to-many)	A supplier can receive many purchase orders.

Category -> Product	(one-to-many)	A category groups many products.

Purchase -> PurchaseItem	(one-to-many)	A purchase has at least one line item.
Sale → SaleItem	one-to-many	A sale has at least one line item.

Product -> PurchaseItem / SaleItem	(one-to-many)	A product can appear in many purchases and sales over time.

User -> Purchase / Sale	(one-to-many)	A user records many purchases and processes many sales.

User -> Password	(one-to-one) -	A user has at most one password record. The unique constraint on Password.user_id enforces this.