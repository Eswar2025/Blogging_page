Case Study 7: Inventory and Warehouse Management System
27 Oct 2026 · @Shajith
Part 1: Requirement Analysis and Database Design
Name
Roll No
Subject

____________
Database Management Systems
1. Problem overview
A multinational manufacturing company tracks its inventory in spreadsheets. It wants a database system that manages products, categories, suppliers, warehouses, inventory, purchase orders, purchase items, goods receipts, stock transfers, dispatches and stock adjustments. The system must show live stock levels and support procurement analysis, warehouse utilization, stock movement tracking and management reports.
The design keeps the number of tables small (13 relations). Every table maps to one element of the ER diagram, so the diagram and the database match one to one.
2. Functional requirements
ID
Requirement
Description
FR1
Manage products and categories
Add, update, delete and search products. Each product is placed in one category.
FR2
Manage suppliers
Store supplier details, a contact person, email and one or more phone numbers.
FR3
Manage warehouses
Store each warehouse with its location (city, country) and storage capacity.
FR4
Track inventory
Keep the current quantity of every product in every warehouse.
FR5
Create purchase orders
Raise a purchase order to one supplier with one or more purchase items, and track its status.
FR6
Record goods receipts
Record goods received against a purchase item. Allow partial deliveries and record rejected quantity. Stock goes up.
FR7
Record stock transfers
Move stock from one warehouse to another. Stock goes down at the source and up at the destination.
FR8
Record dispatches
Record goods sent out to customers. Stock goes down.
FR9
Record stock adjustments
Correct stock for damage, loss, expiry or a physical count difference, with a reason.
FR10
Real-time inventory monitoring
Show stock on hand per product and warehouse, and flag products at or below the reorder level.
FR11
Procurement analysis
Report spending per supplier, pending and partially received orders, and ordered vs received quantity.
FR12
Warehouse utilization
Compare total stock in each warehouse with its capacity.
FR13
Stock movement tracking
Show the full history of stock changes for any product or warehouse.
FR14
Management reporting
Produce summary reports (stock value, top moving products, adjustment losses) from the stored data.
3. Business rules
ID
Business rule
BR1
Every product belongs to exactly one category. A category can have zero or many products.
BR2
Each product has a unique SKU (stock keeping unit code).
BR3
There is only one inventory record for each product in each warehouse. Quantity on hand can never be negative.
BR4
When quantity on hand is at or below the product's reorder level, the product is shown as low stock.
BR5
Total stock stored in a warehouse must not go above the warehouse capacity.
BR6
A purchase order is placed with exactly one supplier. A supplier can receive many purchase orders.
BR7
A purchase order must contain at least one purchase item. Line numbers are unique only inside their own order.
BR8
Ordered quantity must be greater than zero. Unit cost cannot be negative.
BR9
The order total is not stored. It is calculated as the sum of Qty_Ordered x Unit_Cost of its items.
BR10
Goods may arrive in parts, so one purchase item can have many goods receipts. The total received cannot be more than the ordered quantity, and the received product must be the same as the ordered product.
BR11
Rejected quantity is not added to stock. Only the accepted quantity increases inventory.
BR12
Every change to stock is saved as a stock movement. Each movement is exactly one type: goods receipt, dispatch, stock adjustment or stock transfer.
BR13
A dispatch or a transfer cannot take out more stock than is available in the source warehouse.
BR14
A stock transfer must go to a different warehouse than the source warehouse.
BR15
Every adjustment needs a reason (Damage, Loss, Expiry, Count correction) and a direction (Increase or Decrease).
BR16
Purchase order status is one of: Pending, Approved, Partially Received, Received, Cancelled.
Effect of each movement type on stock
Movement type
Source warehouse (Warehouse_ID)
Destination warehouse
Goods receipt
+ Quantity
-
Dispatch
- Quantity
-
Stock adjustment
+ Quantity (Increase) or - Quantity (Decrease)
-
Stock transfer
- Quantity
+ Quantity at To_Warehouse_ID
4. Entities and attributes
4.1 Case study items and where they appear in the design
Case study item
Design element
Kind
Products
PRODUCT
Strong entity
Categories
CATEGORY
Strong entity
Suppliers
SUPPLIER
Strong entity
Warehouses
WAREHOUSE
Strong entity
Inventory
STOCKED_IN (aggregated as [INVENTORY])
M:N relationship between PRODUCT and WAREHOUSE
Purchase orders
PURCHASE_ORDER
Strong entity
Purchase items
PURCHASE_ITEM
Weak entity, owner is PURCHASE_ORDER
Goods receipts
GOODS_RECEIPT
Subclass of STOCK_MOVEMENT
Stock transfers
STOCK_TRANSFER
Subclass of STOCK_MOVEMENT
Dispatches
DISPATCH
Subclass of STOCK_MOVEMENT
Stock adjustments
STOCK_ADJUSTMENT
Subclass of STOCK_MOVEMENT
(added for tracking)
STOCK_MOVEMENT
Superclass. Holds the common data of all four movement types
4.2 Entity types and their attributes
Bold = key attribute. { } = multivalued. Attributes in ( ) after a name are parts of a composite attribute.
Entity
Type
Attributes
Identifier
CATEGORY
Strong
Category_ID, Category_Name, Description
Category_ID
PRODUCT
Strong
Product_ID, Product_Name, SKU, Unit_Price, Reorder_Level
Product_ID (SKU is also unique)
SUPPLIER
Strong
Supplier_ID, Supplier_Name, Contact_Person, Email, {Phone_No} (multivalued)
Supplier_ID
WAREHOUSE
Strong
Warehouse_ID, Warehouse_Name, Capacity, Location (City, Country) (composite)
Warehouse_ID
PURCHASE_ORDER
Strong
PO_ID, Order_Date, Expected_Date, Status, Total_Amount (derived)
PO_ID
PURCHASE_ITEM
Weak (owner: PURCHASE_ORDER)
Line_No (partial key), Qty_Ordered, Unit_Cost
PO_ID + Line_No
STOCK_MOVEMENT
Superclass
Movement_ID, Movement_Date, Quantity, Movement_Type (discriminator)
Movement_ID
GOODS_RECEIPT
Subclass
Qty_Rejected (plus all STOCK_MOVEMENT attributes)
Movement_ID (inherited)
DISPATCH
Subclass
Customer_Name, Destination
Movement_ID (inherited)
STOCK_ADJUSTMENT
Subclass
Reason, Adjust_Type
Movement_ID (inherited)
STOCK_TRANSFER
Subclass
Transfer_Status
Movement_ID (inherited)
STOCKED_IN [INVENTORY]
Relationship (aggregated)
Qty_On_Hand, Last_Updated
Product_ID + Warehouse_ID
4.3 Design decisions
Decision
Reason
Inventory as a relationship
Inventory has no identity of its own. It is the quantity of one product in one warehouse, so it is the M:N relationship STOCKED_IN with the attributes Qty_On_Hand and Last_Updated.
Aggregation [INVENTORY]
A stock movement changes the stock of one product in one warehouse, which is one STOCKED_IN instance. To relate STOCK_MOVEMENT to that pair, STOCKED_IN is treated as a higher-level entity (aggregation).
Purchase item as a weak entity
A purchase item cannot exist without its order. It is identified by the order's PO_ID plus its own Line_No.
Movements as a specialization
Receipts, dispatches, adjustments and transfers all have a date, a quantity, a product and a warehouse. These common attributes sit in STOCK_MOVEMENT, and each subclass keeps only its own extra data. The specialization is disjoint (a movement has one type) and total (every movement has a type). One table now holds the full stock history.
Derived total
Total_Amount of a purchase order is derived from its items, so it is not stored. This avoids update errors.
5. Relationships and cardinalities
The (min,max) pair is written next to the entity it belongs to. It tells how many times one instance of that entity takes part in the relationship. min = 1 means total participation (double line in the diagram).
Relationship
Entities with (min,max)
Ratio
Participation
Meaning
BELONGS_TO
CATEGORY (0,N) : PRODUCT (1,1)
1 : N
Product side total
A category groups many products. A product is in one category.
STOCKED_IN
PRODUCT (0,N) : WAREHOUSE (0,N)
M : N
Both partial
A product can be stored in many warehouses and a warehouse stores many products. Attributes: Qty_On_Hand, Last_Updated.
PLACED_WITH
SUPPLIER (0,N) : PURCHASE_ORDER (1,1)
1 : N
Order side total
Each order goes to exactly one supplier.
CONTAINS (identifying)
PURCHASE_ORDER (1,N) : PURCHASE_ITEM (1,1)
1 : N
Both total
An order has at least one item. An item belongs to one order.
ORDERS
PRODUCT (0,N) : PURCHASE_ITEM (1,1)
1 : N
Item side total
Each purchase item orders one product.
RECEIVED_AGAINST
PURCHASE_ITEM (0,N) : GOODS_RECEIPT (1,1)
1 : N
Receipt side total
One item can be received in several parts. Each receipt is for one item.
AFFECTS
[INVENTORY] (0,N) : STOCK_MOVEMENT (1,1)
1 : N
Movement side total
Each movement changes one product's stock in one warehouse.
TRANSFER_TO
WAREHOUSE (0,N) : STOCK_TRANSFER (1,1)
1 : N
Transfer side total
Each transfer has one destination warehouse.
Specialization (d)
STOCK_MOVEMENT to GOODS_RECEIPT, DISPATCH, STOCK_ADJUSTMENT, STOCK_TRANSFER
IS-A
Disjoint, total
Discriminator attribute: Movement_Type.
6. ER diagram
The EER diagram uses the same notation as the reference diagram: rectangles for entities, double rectangles for weak entities, diamonds for relationships, double diamonds for identifying relationships, ovals for attributes, a circle with d for disjoint specialization and a dashed box for aggregation. Every entity, relationship and attribute in it appears in the relational schema in Section 8.
 
To change the diagram, edit the draw.io file (er_diagram.drawio) at diagrams.net, export a new PNG, and replace this image.
7. ER to relational mapping
EER element
Mapping rule
Result in this design
Strong entities
One table each. The key attribute becomes the primary key.
CATEGORY, PRODUCT, SUPPLIER, WAREHOUSE, PURCHASE_ORDER
Composite attribute
Keep only the simple parts as columns.
Location becomes City, Country in WAREHOUSE
Multivalued attribute
New table with the owner key plus the value. Both together form the primary key.
SUPPLIER_PHONE(Supplier_ID, Phone_No)
Derived attribute
Not stored. Calculated in a query when needed.
Total_Amount = SUM(Qty_Ordered x Unit_Cost)
Weak entity
New table. Primary key = owner key + partial key. Owner key is also a foreign key.
PURCHASE_ITEM(PO_ID, Line_No, ...)
1 : N relationship
Put the primary key of the 1 side as a foreign key in the N side table.
Category_ID in PRODUCT, Supplier_ID in PURCHASE_ORDER, Product_ID in PURCHASE_ITEM, (PO_ID, Line_No) in GOODS_RECEIPT, To_Warehouse_ID in STOCK_TRANSFER
M : N relationship
New table with both primary keys as a composite primary key, plus the relationship attributes.
INVENTORY(Product_ID, Warehouse_ID, Qty_On_Hand, Last_Updated)
Aggregation
The aggregated relationship's table acts as an entity. The 1 : N AFFECTS relationship adds its key as a foreign key.
(Product_ID, Warehouse_ID) in STOCK_MOVEMENT references INVENTORY
Specialization (disjoint, total)
One table for the superclass and one per subclass. Subclass primary key = superclass key, also a foreign key.
STOCK_MOVEMENT, GOODS_RECEIPT, DISPATCH, STOCK_ADJUSTMENT, STOCK_TRANSFER
8. Relational schema
8.1 Simplified relations
Bold = primary key. Italic = foreign key. Bold italic = both.
1. CATEGORY (Category_ID, Category_Name, Description)
2. PRODUCT (Product_ID, Product_Name, SKU, Unit_Price, Reorder_Level, Category_ID)
3. WAREHOUSE (Warehouse_ID, Warehouse_Name, City, Country, Capacity)
4. INVENTORY (Product_ID, Warehouse_ID, Qty_On_Hand, Last_Updated)
5. SUPPLIER (Supplier_ID, Supplier_Name, Contact_Person, Email)
6. SUPPLIER_PHONE (Supplier_ID, Phone_No)
7. PURCHASE_ORDER (PO_ID, Order_Date, Expected_Date, Status, Supplier_ID)
8. PURCHASE_ITEM (PO_ID, Line_No, Product_ID, Qty_Ordered, Unit_Cost)
9. STOCK_MOVEMENT (Movement_ID, Movement_Date, Quantity, Movement_Type, Product_ID, Warehouse_ID)
10. GOODS_RECEIPT (Movement_ID, PO_ID, Line_No, Qty_Rejected)
11. DISPATCH (Movement_ID, Customer_Name, Destination)
12. STOCK_ADJUSTMENT (Movement_ID, Reason, Adjust_Type)
13. STOCK_TRANSFER (Movement_ID, To_Warehouse_ID, Transfer_Status)
8.2 Table structures
Table 1: CATEGORY
Column
Data type
Constraints
Category_ID
INT
PRIMARY KEY
Category_Name
VARCHAR(50)
NOT NULL, UNIQUE
Description
VARCHAR(200)

Table 2: PRODUCT
Column
Data type
Constraints
Product_ID
INT
PRIMARY KEY
Product_Name
VARCHAR(100)
NOT NULL
SKU
VARCHAR(30)
NOT NULL, UNIQUE
Unit_Price
DECIMAL(10,2)
CHECK (Unit_Price >= 0)
Reorder_Level
INT
DEFAULT 0, CHECK (Reorder_Level >= 0)
Category_ID
INT
NOT NULL, FOREIGN KEY references CATEGORY(Category_ID)
Table 3: WAREHOUSE
Column
Data type
Constraints
Warehouse_ID
INT
PRIMARY KEY
Warehouse_Name
VARCHAR(100)
NOT NULL
City
VARCHAR(50)
NOT NULL
Country
VARCHAR(50)
NOT NULL
Capacity
INT
NOT NULL, CHECK (Capacity > 0)
Table 4: INVENTORY
Column
Data type
Constraints
Product_ID
INT
PRIMARY KEY (part), FOREIGN KEY references PRODUCT(Product_ID)
Warehouse_ID
INT
PRIMARY KEY (part), FOREIGN KEY references WAREHOUSE(Warehouse_ID)
Qty_On_Hand
INT
NOT NULL, DEFAULT 0, CHECK (Qty_On_Hand >= 0)
Last_Updated
DATETIME
NOT NULL
Table 5: SUPPLIER
Column
Data type
Constraints
Supplier_ID
INT
PRIMARY KEY
Supplier_Name
VARCHAR(100)
NOT NULL
Contact_Person
VARCHAR(100)

Email
VARCHAR(100)
UNIQUE
Table 6: SUPPLIER_PHONE
Column
Data type
Constraints
Supplier_ID
INT
PRIMARY KEY (part), FOREIGN KEY references SUPPLIER(Supplier_ID)
Phone_No
VARCHAR(15)
PRIMARY KEY (part)
Table 7: PURCHASE_ORDER
Column
Data type
Constraints
PO_ID
INT
PRIMARY KEY
Order_Date
DATE
NOT NULL
Expected_Date
DATE
CHECK (Expected_Date >= Order_Date)
Status
VARCHAR(20)
NOT NULL, CHECK (Status IN ('Pending', 'Approved', 'Partially Received', 'Received', 'Cancelled'))
Supplier_ID
INT
NOT NULL, FOREIGN KEY references SUPPLIER(Supplier_ID)
Table 8: PURCHASE_ITEM
Column
Data type
Constraints
PO_ID
INT
PRIMARY KEY (part), FOREIGN KEY references PURCHASE_ORDER(PO_ID) ON DELETE CASCADE
Line_No
INT
PRIMARY KEY (part)
Product_ID
INT
NOT NULL, FOREIGN KEY references PRODUCT(Product_ID)
Qty_Ordered
INT
NOT NULL, CHECK (Qty_Ordered > 0)
Unit_Cost
DECIMAL(10,2)
NOT NULL, CHECK (Unit_Cost >= 0)
Table 9: STOCK_MOVEMENT
Column
Data type
Constraints
Movement_ID
INT
PRIMARY KEY
Movement_Date
DATETIME
NOT NULL
Quantity
INT
NOT NULL, CHECK (Quantity > 0)
Movement_Type
VARCHAR(12)
NOT NULL, CHECK (Movement_Type IN ('RECEIPT', 'DISPATCH', 'ADJUSTMENT', 'TRANSFER'))
Product_ID
INT
NOT NULL
Warehouse_ID
INT
NOT NULL. (Product_ID, Warehouse_ID) is a FOREIGN KEY references INVENTORY(Product_ID, Warehouse_ID)
Table 10: GOODS_RECEIPT
Column
Data type
Constraints
Movement_ID
INT
PRIMARY KEY, FOREIGN KEY references STOCK_MOVEMENT(Movement_ID)
PO_ID
INT
NOT NULL
Line_No
INT
NOT NULL. (PO_ID, Line_No) is a FOREIGN KEY references PURCHASE_ITEM(PO_ID, Line_No)
Qty_Rejected
INT
DEFAULT 0, CHECK (Qty_Rejected >= 0)
Table 11: DISPATCH
Column
Data type
Constraints
Movement_ID
INT
PRIMARY KEY, FOREIGN KEY references STOCK_MOVEMENT(Movement_ID)
Customer_Name
VARCHAR(100)
NOT NULL
Destination
VARCHAR(150)
NOT NULL
Table 12: STOCK_ADJUSTMENT
Column
Data type
Constraints
Movement_ID
INT
PRIMARY KEY, FOREIGN KEY references STOCK_MOVEMENT(Movement_ID)
Reason
VARCHAR(20)
NOT NULL, CHECK (Reason IN ('Damage', 'Loss', 'Expiry', 'Count correction'))
Adjust_Type
VARCHAR(10)
NOT NULL, CHECK (Adjust_Type IN ('Increase', 'Decrease'))
Table 13: STOCK_TRANSFER
Column
Data type
Constraints
Movement_ID
INT
PRIMARY KEY, FOREIGN KEY references STOCK_MOVEMENT(Movement_ID)
To_Warehouse_ID
INT
NOT NULL, FOREIGN KEY references WAREHOUSE(Warehouse_ID)
Transfer_Status
VARCHAR(15)
NOT NULL, CHECK (Transfer_Status IN ('In transit', 'Completed'))
9. Primary and foreign keys
Table
Primary key
Foreign key(s) → referenced table
CATEGORY
Category_ID
-
PRODUCT
Product_ID
Category_ID → CATEGORY
WAREHOUSE
Warehouse_ID
-
INVENTORY
(Product_ID, Warehouse_ID)
Product_ID → PRODUCT; Warehouse_ID → WAREHOUSE
SUPPLIER
Supplier_ID
-
SUPPLIER_PHONE
(Supplier_ID, Phone_No)
Supplier_ID → SUPPLIER
PURCHASE_ORDER
PO_ID
Supplier_ID → SUPPLIER
PURCHASE_ITEM
(PO_ID, Line_No)
PO_ID → PURCHASE_ORDER; Product_ID → PRODUCT
STOCK_MOVEMENT
Movement_ID
(Product_ID, Warehouse_ID) → INVENTORY
GOODS_RECEIPT
Movement_ID
Movement_ID → STOCK_MOVEMENT; (PO_ID, Line_No) → PURCHASE_ITEM
DISPATCH
Movement_ID
Movement_ID → STOCK_MOVEMENT
STOCK_ADJUSTMENT
Movement_ID
Movement_ID → STOCK_MOVEMENT
STOCK_TRANSFER
Movement_ID
Movement_ID → STOCK_MOVEMENT; To_Warehouse_ID → WAREHOUSE
Candidate keys: SKU in PRODUCT, Category_Name in CATEGORY and Email in SUPPLIER are also unique, so each is a candidate key. They are not chosen as primary keys because a short integer ID never changes and keeps the foreign keys small.
10. Requirement coverage check
Each reporting need from the case study is answered by the tables below, so no extra table is needed.
Need
Tables used
How
Real-time inventory monitoring
INVENTORY, PRODUCT, WAREHOUSE
Qty_On_Hand per product and warehouse. Low stock when Qty_On_Hand <= Reorder_Level.
Procurement analysis
PURCHASE_ORDER, PURCHASE_ITEM, GOODS_RECEIPT, STOCK_MOVEMENT, SUPPLIER
Spend per supplier = SUM(Qty_Ordered x Unit_Cost). Ordered vs received = Qty_Ordered compared with SUM(Quantity) of its receipts.
Warehouse utilization
INVENTORY, WAREHOUSE
SUM(Qty_On_Hand) / Capacity for each warehouse.
Stock movement tracking
STOCK_MOVEMENT and its four subclass tables
All stock changes in date order, filtered by product, warehouse or Movement_Type.
Management reporting
All tables
Stock value (Qty_On_Hand x Unit_Price), top dispatched products, losses from adjustments.