# Experiment 2: DDL Commands
## NAME: CH.DINESH KUMAR
## REG NO: 212224040055

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
```
In the Cusomers table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

CustomerID  Name          Address      City        ZipCode
----------  ------------  ----------   ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Manor  Gotham      10007
308         Peter Parker  Queens                   11375
```
```sql
insert into Customers(CustomerID,Name,Address,City,ZipCode)
values (306,'Diana Prince','Themyscira',NULL,NULL),(307,'Bruce Wayne','Wayne Mano','Gotham',10007),(308,'Peter Parkers','Queens',NULL,'11375')
```

**Output:**

<img width="1290" height="287" alt="image" src="https://github.com/user-attachments/assets/c855d453-f645-44b6-9a44-a70b928215ee" />


**Question 2**
```
Write a SQL Query  to add attribute ISBN as varchar(30) and domain_dept as varchar(30) in the table 'books'

 

 

For example:

Test	Result
pragma table_info('books');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           book_id     INT         0                       1
1           title       VARCHAR(15  0                       0
2           author      VARCHAR(10  0                       0
3           genre       VARCHAR(50  0                       0
4           publicatio  INT         0                       0
5           ISBN        varchar(30  0                       0
6           domain_dep  varchar(30  0                       0

```

```sql
ALTER TABLE books
ADD COLUMN ISBN varchar(30);
ALTER TABLE books
ADD COLUMN domain_dept varchar(30);
```

**Output:**

<img width="1303" height="296" alt="image" src="https://github.com/user-attachments/assets/ac347274-0ef4-465d-88d7-706a24e9987e" />


**Question 3**
```
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);
SELECT * FROM Invoices;
InvoiceID   InvoiceDate  Amount      DueDate     OrderID
----------  -----------  ----------  ----------  ----------
1           2024-08-01   100.0       2024-09-01  1
```


```sql
CREATE TABLE Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE NOT NULL,
Amount REAL CHECK (Amount>0),
DueDate DATE CHECK (DueDate>InvoiceDate),
OrderID INTEGER,
FOREIGN KEY (OrderID) REFERENCES
Orders(OrderID)
)
```

**Output:**
<img width="1180" height="170" alt="image" src="https://github.com/user-attachments/assets/ddf8a8d4-57bd-46d3-aaff-744ea5640f88" />


**Question 4**
```
Create a new table named orders with the following specifications:
ord_id as TEXT with a length of 4.
item_id as TEXT.
ord_date as DATE.
ord_qty as INTEGER.
cost as INTEGER.
The primary key is a composite key consisting of item_id and ord_date.
ord_id and item_id should not accept NULL
For example:

Test	Result
INSERT INTO orders (ord_id, item_id, ord_date, ord_qty, cost) VALUES ('O001', 'I001', '2023-08-01', 10, 100);
SELECT * FROM orders;
ord_id      item_id     ord_date    ord_qty     cost
----------  ----------  ----------  ----------  ----------
O001        I001        2023-08-01  10          100

```

```sql
CREATE TABLE orders(
ord_id TEXT CHECK (LENGTH(ord_id)=4) NOT NULL,
item_id TEXT NOT NULL,
ord_date DATE ,
ord_qty INTEGER,
cost INTEGER,
PRIMARY KEY (item_id,ord_date)
);
```

**Output:**

<img width="1167" height="196" alt="image" src="https://github.com/user-attachments/assets/cc27c4f6-08dc-4d64-80a9-fe3c682cd46e" />


**Question 5**
```
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700         COM5



```

```sql
CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT(4) CHECK (LENGTH(icom_id)=4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
        ON UPDATE CASCADE
        ON DELETE CASCADE
    
);
```

**Output:**

<img width="800" height="216" alt="image" src="https://github.com/user-attachments/assets/725e8762-3c55-4f5d-9ed0-e6053d1dbb73" />


**Question 6**
```
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.
 
 
For example:

Test	Result
SELECT ISBN, Title, Author
FROM Books 


ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

```

```sql
INSERT INTO Books (ISBN ,Title , Author)
VALUES ('978-6655443321' ,'Big Data Analytics','Karen Adams');
```

**Output:**

<img width="774" height="203" alt="image" src="https://github.com/user-attachments/assets/fd16a8e1-6cfd-4193-b9fa-53a9e29ee546" />


**Question 7**
```
Write a SQL Query  to change the name of attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date in the table Companies. 

 

 

For example:

Test	Result
pragma table_info('Companies');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          int         0                       0
1           first_name  varchar(50  0                       0
2           address     text        0                       0
3           email       varchar(50  0                       0
4           phone       varchar(10  0                       0
5           mobilenumb  number      0                       0
6           DOB         Date        0                       0

```

```sql
ALTER table Companies rename column name TO first_name;
ALTER table Companies add column mobilenumber number;
ALTER table Companies add column DOB Date;
```

**Output:**

<img width="1088" height="231" alt="image" src="https://github.com/user-attachments/assets/91664306-9de6-4665-b6a7-f4f15e730194" />


**Question 8**
```
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

For example:

Test	Result
select * from Books;
ISBN            Title           Author              Publisher      YearPublished
--------------  --------------  ------------------  -------------  -------------
978-1234567890  The Lost World  Arthur Conan Doyle  Vintage Books  1912
978-0987654321  Gone with the   Margaret Mitchell   Macmillan      1936
978-1122334455  Moby Dick       Herman Melville     Harper & Brot  1851
```

```sql
insert into Books(ISBN,Title,Author,Publisher,YearPublished)
SELECT ISBN,Title,Author,Publisher,YearPublished from Out_of_print_books
```

**Output:**

<img width="973" height="172" alt="image" src="https://github.com/user-attachments/assets/dcf45f53-5710-4175-9535-b69b43e2ae52" />


**Question 9**
```
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
For example:

Test	Result
INSERT INTO Products
VALUES (1, NULL,0,5);
Error: NOT NULL constraint failed: Products.ProductName

```
```sql
CREATE TABLE Products(ProductID PRIMARY KEY,ProductName NOT NULL,Price real check(price>0),Stock INTEGER CHECK(Stock>=0));
```

**Output:**

<img width="789" height="187" alt="image" src="https://github.com/user-attachments/assets/dc49fd60-0533-4f84-9231-a0f0d18ae969" />


**Question 10**
```
Create a table named Products with the following columns:

ProductID as INTEGER
ProductName as TEXT
Price as REAL
Stock as INTEGER
For example:

Test	Result
pragma table_info('Products');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     ProductID   INTEGER     0                       0
1     ProductNam  TEXT        0                       0
2     Price       REAL        0                       0
3     Stock       INTEGER     0                       0

```

```sql
CREATE TABLE Products(ProductID INTEGER,ProductName TEXT,Price REAL check(price>0),Stock INTEGER CHECK(Stock>=0));
```

**Output:**


<img width="884" height="192" alt="image" src="https://github.com/user-attachments/assets/e14af878-29f0-4644-ab3a-5c1af2b68bbd" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
