# Experiment 4: Aggregate Functions, Group By and Having Clause
## NAME:CHITLURU VENKATA SIVA DINESH KUMAR
## REG NO: 212224040055
 
## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**

```

Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table



For example:

Result
PatientID   AvgMedications
----------  --------------
4           5
6           1
7           1
8           3

```
```sql
select PatientID,count(Medications) as AvgMedications from MedicalRecords
group by PatientID
```

**Output:**

<img width="620" height="550" alt="image" src="https://github.com/user-attachments/assets/b4ab13e7-6b43-4904-a5ad-9d9f836bf295" />


**Question 2**
```

What is the total number of appointments scheduled for each day?

Table: Appointments

name                 type
-------------------  ----------
AppointmentID        INTEGER
PatientID            INTEGER
DoctorID             INTEGER
AppointmentDateTime  DATETIME
Purpose              TEXT
Status               TEXT
 

For example:

Result
AppointmentDate  TotalAppointments
---------------  -----------------
2024-02-16       4
2024-02-18       1
2024-02-20       1
2024-02-21       1
2024-02-22       1
2024-02-23       2

```
```sql
SELECT DATE(AppointmentDateTime) AS AppointmentDate, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DATE(AppointmentDateTime)
ORDER BY DATE(AppointmentDateTime);
```

**Output:**

<img width="771" height="553" alt="image" src="https://github.com/user-attachments/assets/9ebdbb54-6de8-4094-a973-f290aef11c0f" />




**Question 3**
```
What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table



For example:

Result
DoctorID    TotalAppointments
----------  -----------------
1           1
2           3
5           3
9           2
10          1

```
```sql
SELECT DoctorID, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID;
```

**Output:**

<img width="727" height="547" alt="image" src="https://github.com/user-attachments/assets/c1928748-3c75-4e90-a1f3-a4faeba84c5b" />


**Question 4**

```

<img width="731" height="377" alt="image" src="https://github.com/user-attachments/assets/2df5ec5b-61f1-4bac-a965-a2e5966b2aa9" />

```

```sql
SELECT COUNT(*) AS COUNT
FROM customer
WHERE city = 'Noida';
```

**Output:**

<img width="468" height="318" alt="image" src="https://github.com/user-attachments/assets/fc5f3a43-f31d-4e88-b888-e3810c1da645" />


**Question 5**
```
Write a SQL query to find the shortest email address in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
name        email           min_email_length
----------  --------------  ----------------
Ravi Kumar  ravi@gmail.com  14
```

```sql
SELECT name, email, LENGTH(email) AS min_email_length
FROM customer
WHERE LENGTH(email) = (
      SELECT MIN(LENGTH(email))
      FROM customer
)
LIMIT 1;
```

**Output:**

<img width="862" height="298" alt="image" src="https://github.com/user-attachments/assets/ec918c21-1d13-4cde-8e64-0c00c77f5651" />


**Question 6**
```

Write a SQL query to find the customer with longest name?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
name          length
------------  ----------
Preeti Patel  12

```

```sql
SELECT name, LENGTH(name) AS length
FROM customer
ORDER BY length DESC
LIMIT 1;
```

**Output:**

<img width="635" height="310" alt="image" src="https://github.com/user-attachments/assets/1f3cf9f1-52b1-4f3c-be69-86697d4641ac" />


**Question 7**
```
Write a SQL query to calculate total purchase amount of all orders. Return total purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

For example:

Result
TOTAL
----------
17541.18


```sql

select sum(purch_amt) as TOTAL from orders!

```

**Output:**


<img width="477" height="297" alt="image" src="https://github.com/user-attachments/assets/d95eb0e3-d9c3-4733-84ae-1d3cc11ce074" />


**Question 8**
```

Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 1,000,000.

Sample table: employee



For example:

Result
age         Income
----------  ----------
32          200000
40          350000
45          450000

```

```sql
SELECT age, MIN(income) AS "Income"
FROM employee
GROUP BY age
HAVING MIN(income) < 600000;
```

**Output:**


<img width="637" height="412" alt="image" src="https://github.com/user-attachments/assets/d42f88f5-3d3e-4b8e-a4f5-f634a0af8b48" />


**Question 9**
```
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the total work hours for each date, and excludes dates where the total work hour sum is not greater than 40.

Sample table: employee1



For example:

Result
jdate       SUM(workhour)
----------  -------------
2004.0      46
2006.0      46

```

```sql
select jdate,SUM(workhour)
from employee1
group by jdate
having SUM(workhour)>40;
```

**Output:**


<img width="571" height="385" alt="image" src="https://github.com/user-attachments/assets/c14247ef-08bb-4ee9-8f56-398b745ab7d4" />


**Question 10**
```
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products



For example:

Result
category_id  count(product_name)
-----------  -------------------
1            4
2            3
```

```sql
SELECT category_id ,count(product_name)
FROM products
GROUP BY category_id
HAVING MIN(category_id)<3;
```

**Output:**


<img width="631" height="341" alt="image" src="https://github.com/user-attachments/assets/50b98e0c-af6f-462d-aa10-38edb641fd61" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
