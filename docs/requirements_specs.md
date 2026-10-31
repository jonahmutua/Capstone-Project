
# Inventory Management System with intelliegent restocking engine

# System Requirements Specification 


## 1. Introduction 

### 1.1 Purpose 

This document specifies the requirements for a  Management System (SIMS). It defines what the system must do, the rules it must follow, and the qualities it must have, so that design, development and testing can proceed from a shared understanding. It does not prescribe technology, those choices come in the design phase. 

### 1.2 Scope 

 Inventory Management System with Intelligent auto restock engine lets a small business owners track their products, suppliers, purchases (stock coming in) and sales (stock going out), and keeps stock levels accurate as these happen. Its distinguishing feature is an Intelligent Restocking Engine that calculates daily demand for each product and recommends what to reorder, how much, and why. 
 

### 1.3 Definitions 

- **On hand** : units currently in stock. 

- **On order** : units ordered from a supplier but not yet received. 

- **Lead time** : days between placing an order with a supplier and receiving it. 

- **Safety stock** : extra units kept as a buffer against demand variation and delivery delays. 
- **Reorder point** : the stock level at or below which a product needs restocking. 

- **Cover days** : days of sales an incoming order should last after it arrives. 

- **SKU / product** : one distinct item sold, identified by a unique barcode. 



### 1.4 Intended audience 

The business owners and developers.

## 2. Overall description 

### 2.1 Product perspective 

Inventory Management System with intelliegent restocking engine is a standalone application with its own database. 

### 2.2 User classes 

|Role|Description|Typical tasks|
|---|---|---|
|Admin|System owner|Manage users, roles and master data; full access|
|Manager|Store or inventory<br>manager|Review and approve restock recommendations,<br>manage suppliers and prices, view reports|
|Stock clerk|Warehouse or shelf staff|Record purchases and receipts, update product details, check stock|
|Cashier|Checkout staff|Record sales only|



### 2.3 Operating environment 

A browser-based application used on store computers and tablets, with a relational database.

### 2.4 Constraints . 

- Each product has one default supplier. 

- Categories are flat (no subcategories). 

- Every product carries a unique barcode. 

- Sales are recorded at the time they occur, so sales history is reliable enough to measure demand. 

- Supplier lead times are known and stable enough to be stored as a single number per supplier. 

- The store has a working internet or local network connection. 

## 3. Functional requirements 

Priority key: **M** = must have , **S** = should have, **C** = could have. 

### 3.1 Authentication and user management 

|ID|Requirement|Priority|
|---|---|---|
|FR-AUTH-01|The system shall require a username and password to log in.|M|
|FR-AUTH-02|Passwords shall be stored only in hashed form in<br>a separate Password record, one per user.|M|
|FR-AUTH-03|The system shall restrict each function to the roles<br>permitted in section 3.10.|M|
|FR-AUTH-04|The system shall end inactive sessions after a<br>configurable period.|S|
|FR-AUTH-05|The system shall lock an account temporarily after<br>repeated failed log-ins.|S|
|FR-USR-01|An Admin shall be able to create users with a full<br>name, unique username, role and initial password.|M|
|FR-USR-02|An Admin shall be able to edit a user's name and<br>role, and activate or deactivate a user. Users shall<br>never be deleted, so past records stay valid.|M|
|FR-USR-03|Deactivated users shall not be able to log in.|M|
|FR-USR-04|A user shall be able to change their own password;<br>an Admin shall be able to reset any password.|M|



### 3.2 Category management 

|ID|Requirement|Priority|
|---|---|---|
|FR-CAT-01|The system shall allow creating, viewing and<br>editing categories with a unique name and optional<br>description.|M|
|FR-CAT-02|A category that has products shall not be<br>deletable.|M|


### 3.3 Supplier management 

|ID|Requirement|Priority|
|---|---|---|
|FR-SUP-01|The system shall allow creating, viewing and<br>editing suppliers with name, phone, email and<br>address.|M|
|FR-SUP-02|Each supplier shall have a lead time in days, which<br>must be a whole number of at least 0.|M|
|FR-SUP-03|A supplier that has products or purchases shall not<br>be deletable.|M|
|FR-SUP-04|The system shall show a supplier's products and<br>purchase history.|S|



### 3.4 Product management 

|ID|Requirement|Priority|
|---|---|---|
|FR-PRD-01|The system shall allow creating and editing<br>products with name, unique barcode, category,<br>default supplier, selling price, cost price, reorder<br>level, reorder quantity and safety stock.|M|
|FR-PRD-02|Stock on hand shall change only through recorded<br>sales, received purchases or authorised stock<br>adjustments, never by free editing.|M|
|FR-PRD-03|The system shall allow searching and filtering<br>products by name, barcode, category and supplier.|M|
|FR-PRD-04|The system shall highlight products whose on-hand<br>quantity is at or below their reorder point.|S|
|FR-PRD-05|A product that appears in any sale or purchase<br>shall not be deletable.|M|
|FR-PRD-06|A Manager shall be able to change a product's<br>selling price; the change shall apply to future sales<br>only.|M|


### 3.5 Purchase management 

A purchase is an order to one supplier, containing one or more products. 

|ID|Requirement|Priority|
|---|---|---|
|FR-PUR-01|A Stock Clerk or Manager shall be able to create a<br>purchase for one supplier with one or more line<br>items (product, quantity, unit cost).|M|
|FR-PUR-02|A purchase shall have a status: Ordered, Received<br>or Cancelled, and an expected delivery date.|M|
|FR-PUR-03|The expected date shall default to the order date<br>plus the supplier's lead time and be editable.|S|
|FR-PUR-04|When a purchase is marked Received, the system<br>shall add each line quantity to the product's on-<br>hand stock and update the product's cost price to<br>the unit cost paid.|M|
|FR-PUR-05|The purchase total shall be calculated by the<br>system from its line items.|M|
|FR-PUR-06|An Ordered purchase may be edited or cancelled.<br>A Received purchase shall not be edited.|M|
|FR-PUR-07|The system shall record which user created each<br>purchase.|M|
|FR-PUR-08|The system shall list purchases filterable by<br>supplier, status and date range.|S|



### 3.6 Sales management 

|ID|Requirement|Priority|
|---|---|---|
|FR-SAL-01|A Cashier shall be able to create a sale by adding<br>products by barcode or search, with a quantity for<br>each.|M|
|FR-SAL-02|Each sale line shall copy the product's current<br>selling price at the moment of sale.|M|

|ID|Requirement|Priority|
|---|---|---|
|FR-SAL-03|On completing a sale, the system shall reduce each<br>product's on-hand stock by the quantity sold, as<br>one atomic operation.|M|
|FR-SAL-04|The system shall reject a sale line whose quantity<br>exceeds the stock on hand.|M|
|FR-SAL-05|The system shall calculate the sale total from its<br>lines and record the cashier and the date and time.|M|
|FR-SAL-06|Completed sales shall not be edited or deleted.|M|
|FR-SAL-07|The system shall list sales filterable by date range<br>and cashier.|S|



### 3.7 Stock monitoring 

|ID|Requirement|Priority|
|---|---|---|
|FR-STK-01|The system shall display current stock for every<br>product, including quantity on order.|M|
|FR-STK-02|The system shall provide a low-stock view of<br>products at or below their reorder point.|M|
|FR-STK-03|A Manager shall be able to record a stock<br>adjustment (for example damage, expiry or count<br>correction) with a reason.|S|



### 3.8 Intelligent Restocking Engine 

#### Detailed rules are in section 4. 

|ID|Requirement|Priority|
|---|---|---|
|FR-RST-01|The system shall calculate average daily demand<br>for each product from recorded sales over a configurable window (default 30 days).|M|
|FR-RST-02|The system shall calculate each product's reorder<br>point from daily demand, the supplier's lead time<br>and the product's safety stock.|M|
|FR-RST-03|The system shall recommend a restock for every<br>product whose available stock (on hand plus on<br>order) is at or below its reorder point.|M|
|FR-RST-04|Each recommendation shall state the<br>recommended quantity and the supplier to order<br>from.|M|
|FR-RST-05|Each recommendation shall include a plain-<br>language explanation of why that quantity was<br>chosen, using the actual figures.|M|
|FR-RST-06|The system shall store each recommendation with<br>a snapshot of all figures used, so it can be reviewed<br>later.|M|
|FR-RST-07|The engine shall run automatically once a day and<br>on demand by a Manager.|M|
|FR-RST-08|A Manager shall be able to accept, adjust the<br>quantity of, or dismiss each recommendation.|M|
|FR-RST-09|Accepting a recommendation shall create a<br>purchase with status Ordered and link it to the<br>recommendation.|M|
|FR-RST-10|The system shall not create duplicate<br>recommendations for a product that already has a<br>pending one or an open order covering the need.|M|
|FR-RST-11|The system shall allow grouping accepted<br>recommendations by supplier into one purchase<br>per supplier.|S|
|FR-RST-12|A Manager shall be able to view past<br>recommendations and whether they were<br>accepted, adjusted or dismissed.|S|


### 3.9 Reporting 

|ID|Requirement|Priority|
|---|---|---|
|FR-RPT-01|Sales summary by day, product and category for a<br>chosen period.|S|
|FR-RPT-02|Purchase summary by supplier for a chosen period.|S|
|FR-RPT-03|Current stock valuation (on hand multiplied by cost<br>price).|C|
|FR-RPT-04|Top-selling and slow-moving products.|C|



### 3.10 Role permissions 

|Function|Admin|Manager|Stock Clerk|Cashier|
|---|---|---|---|---|
|Manage users|Yes|No|No|No|
|Manage categories|Yes|Yes|No|No|
|Manage suppliers|Yes|Yes|No|No|
|Create or edit products|Yes|Yes|Yes|No|
|Change selling price|Yes|Yes|No|No|
|Create purchases, mark received|Yes|Yes|Yes|No|
|Record sales|Yes|Yes|No|Yes|
|Stock adjustments|Yes|Yes|No|No|
|View and act on restock recommendations|Yes|Yes|View only|No|
|View reports|Yes|Yes|No|No|



## 4. Intelligent Restocking Engine: detailed rules 

### 4.1 Inputs 

- Sales history (sales and their line items) for the demand window. 
 
- Product: on-hand quantity, safety stock, default supplier, fallback reorder level and quantity. 

- Supplier: lead time in days. 

- Open purchases with status Ordered (quantity on order). 

- Settings: demand window (30 days) and cover days (7), held as application constant - (configarable). 

### 4.2 Calculations 

|Quantity|Formula|
|---|---|
|Average daily demand|total units sold in window divided by window days|
|Quantity on order|sum of line quantities of purchases with status<br>Ordered|
|Available stock|quantity on hand|
|Reorder point|daily demand multiplied by lead time days, plus<br>safety stock|
|Recommended quantity|daily demand multiplied by (lead time plus cover<br>days), plus safety stock, minus available stock|



A recommendation is generated when available stock is at or below the reorder point. The recommended quantity is rounded up to a whole number and must be greater than zero. 

### 4.3 Worked example 

Milk: 40 units sold per day, supplier lead time 3 days, safety stock 30, cover days 7, on hand 120, nothing on order. 

- Reorder point = 40 × 3 + 30 = 150. Available stock 120 is at or below 150, so restock. Recommended quantity = 40 × (3 + 7) + 30 − 120 = 310 units. 

### 4.4 Special cases 

|Situation|Behaviour|
|---|---|
|Product has no sales history at all|Use the product's fallback reorder level and<br>reorder quantity; the explanation shall say<br>demand data was unavailable.|
|Product has sales history but none in the<br>window|Daily demand is zero; no recommendation is<br>generated.|
|Product has fewer days of history than the<br>window|Divide by the days of history available, with a<br>minimum of 7 days.|
|Calculated quantity is zero or negative|No recommendation.|
|Product already has an Ordered purchase<br>covering the need|No new recommendation (on-order stock is<br>counted).|
|Product has no default supplier|Flag as an exception for the Manager; no<br>recommendation is generated.|
|Supplier lead time is zero|Calculation proceeds; the explanation states<br>same-day delivery.|



### 4.5 Explanation content 

Every recommendation's explanation shall state, in plain language: the product and supplier, the recommended quantity, the average daily demand and the window it came from, the lead time and what will sell during it, the current stock and any quantity on order, the reorder point and why the product is at or below it, and the safety stock and cover days included in the quantity. 

Example: "Order 310 units of Milk from Fresh Dairy Ltd. Sales average 40 units a day over the last 30 days. Delivery takes 3 days, so about 120 units will sell before it arrives. Stock (120) is at or below the reorder point (150). The order covers lead time plus 7 days of sales and keeps a 30-unit safety buffer." 

### 4.6 Recommendation lifecycle 

Pending, then Accepted (purchase created and linked), or Dismissed. When the engine reruns, a still-pending recommendation for the same product is refreshed with new figures rather than duplicated. Accepted and dismissed recommendations are kept 

#### permanently as history. 

## 5. Data requirements 

### 5.1 Entities 

The system stores ten entities. Their attributes and relationships are defined in the ER diagram. 

|Entity|Purpose|
|---|---|
|Supplier|Who stock is bought from, including lead time|
|Category|Groups products|
|Product|Items sold, with stock level, prices, reorder settings<br>and safety stock|
|Purchase|An order to a supplier, with status and expected<br>date|
|PurchaseItem|Products and quantities on a purchase|
|Sale|A customer transaction|
|SaleItem|Products and quantities on a sale|
|User|A person who logs in, with a role|
|Password|A user's hashed credential, kept separately|
|RestockRecommendation|A restocking suggestion with its figures and<br>explanation|



### 5.2 Data rules 

- Barcodes, usernames and category names must be unique. 

- Quantities on sales and purchases must be positive whole numbers; on-hand stock must never be negative. 

- Monetary values are stored with two decimal places. 

- Prices and costs on line items are copies taken at transaction time and never change afterwards. 

- Sale and purchase totals must equal the sum of their line items. 

Records with history are deactivated or kept, never deleted. 

### 5.3 Retention 

Sales, purchases and recommendations shall be retained for at least five years.

## 6. Business rules 

- **BR-01** : Stock increases only when a purchase is marked Received. 

- **BR-02** : Stock decreases only through completed sales or approved stock adjustments. 

- **BR-03** : A product is restocked from its default supplier unless a Manager changes the purchase supplier. 

- **BR-04** : A sale must never take stock below zero. 

- **BR-05** : A Cancelled purchase has no effect on stock or on-order quantity. 

- **BR-06** : The engine recommends only; a human always decides whether an order is placed. 

- **BR-07** : Every sale and purchase records the user who created it. 

## 7. Non-functional requirements 

### 7.1 Security 

- Passwords hashed with suitable encryption; never logged or displayed. 

- Role-based access enforced on the server side, not only in the interface. 

- Protection against common web attacks (SQL injection, cross-site scripting, cross-site request forgery). 

- All traffic encrypted in transit. 

### 7.2 Performance (proposed targets) 

- Completing a sale in under 2 seconds under normal load. 

- Product search results in under 1 second for up to 10,000 products. 

- A full engine run in under 60 seconds for up to 10,000 products. 


### 7.3 Reliability and data integrity 

- Sales, purchase receipts and recommendation acceptance run as atomic transactions: they fully succeed or fully fail. 

- Automated database backups at least daily, with a tested restore procedure. 

- Recording a sale must not be blocked by the engine running. 

### 7.4 Usability 

- A cashier shall be able to record a typical sale with barcode entry and minimal clicks. Error messages shall say what went wrong and how to fix it. 

- The interface shall work on desktop and tablet screens. 

### 7.5 Auditability 

- Key records carry the creating user and timestamp. 

- Recommendations keep a permanent snapshot of the numbers used. 

### 7.6 Maintainability and extensibility 

- Restocking parameters (window, cover days, and later service level) shall be configurable without code changes where practical. 

- The design shall allow later additions (returns, multiple stores, computed safety stock) without restructuring existing tables. 

## 8. Key use cases 

|ID|Use case|Actor|Summary|
|---|---|---|---|
|UC-01|Log in|All users|Enter credentials; system verifies and opens the role's menu.|
|UC-02|Record a sale|Cashier|Add products by barcode, system prices lines, reduces stock, saves sale.|
|UC-03|Create a purchase|Stock Clerk, Manager|Choose supplier, add products and costs, save as Ordered.|


|ID|Use case|Actor|Summary|
|---|---|---|---|
|UC-<br>04|Receive a purchase|Stock Clerk|Mark order Received; stock and<br>cost prices update.|
|UC-<br>05|Review<br>recommendations|Manager|See pending recommendations with<br>explanations; accept, adjust or<br>dismiss.|
|UC-<br>06|Accept a<br>recommendation|Manager|System creates an Ordered<br>purchase for the supplier and links<br>it.|
|UC-<br>07|Manage products and<br>suppliers|Manager,<br>Admin|Create and edit master data.|
|UC-<br>08|Manage users|Admin|Create users, assign roles,<br>deactivate, reset passwords.|
|UC-<br>09|View reports|Manager|Choose a report and period; system<br>displays results.|



## 9. Acceptance criteria

- Completing a sale of 3 units of a product with 10 on hand leaves 7 on hand; attempting to sell 11 is rejected. 

- Marking a purchase of 100 units Received increases stock by 100 and updates the product's cost price. 

- For the milk example in section 4.3, the engine produces a recommendation for 310 units and an explanation containing the demand, lead time, stock and reorder point figures. 

- Running the engine twice in a day produces one pending recommendation per product, not two. 

- After a recommendation is accepted, the same product is not recommended again while the resulting order is still open and covers the need. 

- A Cashier cannot open the purchase, user or recommendation screens. 

- A deactivated user cannot log in, but their past sales remain visible. 


## 10. Out of scope (future)

- Customer returns, voids and refunds. 

- Customer entity, loyalty and discounts. 

- Multiple stores or warehouses. 

- Multiple suppliers per product and supplier price comparison. 

- Computed safety stock from demand variability and a target service level. 

- Seasonality, promotions and trend-aware demand forecasting. 

- Batch and expiry tracking for perishable goods. 

- Barcode scanner or point-of-sale hardware integration. 

- Automatic emailing of orders to suppliers. 

- Payment processing and accounting integration. 

- A settings screen for restocking parameters. 

