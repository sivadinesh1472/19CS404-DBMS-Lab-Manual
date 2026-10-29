# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---



# Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
 
<img width="4512" height="2190" alt="erdplus (5)" src="https://github.com/user-attachments/assets/d388e235-4e6c-42dd-b69b-78a37ec3d60b" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|---------------------|-------|
| Customer | CustomerID (PK), Name, ContactDetails, TableNumber | Customer details |
| Waiter | WaiterID (PK), Name, ContactDetails | Serves tables and creates orders |
| Chef | ChefID (PK), Name, ContactDetails | Prepares order items |
| Table | TableID (PK), Location, Status | Restaurant table details |
| FoodItem | FoodItemID (PK), Name, Description, Price, Category | Menu items |
| Order | OrderID (PK), DateTime, TotalAmount, Status | Order details |
| OrderItem | OrderItemID (PK), OrderID (FK), FoodItemID (FK), Quantity, Status | Individual order items |
| Bill | BillID (PK), OrderID (FK), TotalAmount, PaymentStatus | Billing and payment details |
| Supervisor | SupervisorID (PK), Name, ContactDetails | Manages exceptional order cases |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| Customer - Table (Has) | Many-to-One | Customer: Total; Table: Partial | A customer is assigned to one table |
| Waiter - Table (Serves) | One-to-Many | Waiter: Partial; Table: Total | A waiter serves multiple tables |
| Waiter - Order (Creates) | One-to-Many | Waiter: Partial; Order: Total | A waiter creates multiple orders |
| Order - Table (Belongs to) | Many-to-One | Order: Total; Table: Partial | An order belongs to one table |
| Order - OrderItem (Contains) | One-to-Many | Both: Total | An order contains multiple order items |
| OrderItem - FoodItem (Refers to) | Many-to-One | OrderItem: Total; FoodItem: Partial | Each order item refers to one food item |
| Order - Bill (Generates) | One-to-One | Order: Partial; Bill: Total | A bill is generated for one order |
| Chef - OrderItem (Prepares) | One-to-Many | Chef: Partial; OrderItem: Total | A chef prepares multiple order items |
| Supervisor - Order (Manages) | One-to-Many | Supervisor: Partial; Order: Partial | A supervisor manages exceptional order cases |

### Assumptions

- Each entity has a unique primary key.
- Foreign keys maintain relationships between entities.
- Each customer is assigned to one table.
- Each order is created by one waiter and belongs to one table.
- Each order contains multiple order items.
- Each order item refers to one food item.
- Each order can have one bill.
- Each order item is prepared by one chef.
- A supervisor oversees exceptional order cases when necessary.


