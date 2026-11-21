# Experiment 5: Subqueries and Views
## NAME : CHITLURU VENKATA SIVA DINESH KUMAR
## REG NO: 212224040055
## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
```
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
id     name             city             email            phone
-----  ---------------  ---------------  ---------------  ----------
6      Aarti Desai      Pune             aarti@gmail.com  890123456
7      Vivek Sharma     Chandigarh       vivek@gmail.com  980154021
8      Nisha Patel      Noida            nisha@gmail.com  901234567
9      Rajesh Singh     Hyderabad        rajesh@gmail.co  917654301

```

```sql
SELECT id, name, city, email, phone
FROM customer
WHERE city != (
    SELECT city
    FROM customer
    WHERE id = (SELECT MAX(id) FROM customer)
);
```

**Output:**


<img width="1135" height="427" alt="image" src="https://github.com/user-attachments/assets/2f2be096-efbb-448a-a39f-60d714c35b51" />


**Question 2**
```
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
name   city
-----  ---------------
Neha   Bangalore
Rohit  Bangalore
Manoj  Bangalore
Vivek  Chandigarh


```

```sql
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city
    FROM customer
    WHERE id IN (3, 7)
);
```

**Output:**


<img width="522" height="417" alt="image" src="https://github.com/user-attachments/assets/564aa182-4379-4871-bc49-9327760a90c3" />


**Question 3**
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
2           Khilan      25          Delhi       1500
```


```sql
SELECT *
FROM CUSTOMERS 
WHERE ADDRESS = 'Delhi' AND AGE < 30
ORDER BY ID ASC;
```

**Output:**


<img width="1067" height="335" alt="image" src="https://github.com/user-attachments/assets/d40c931a-8d0b-4f7d-91eb-3c6a43a26cc2" />


**Question 4**
```
From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
 

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70011       75.29       2012-08-17  3003         5007


```

```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM orders o
JOIN salesman s ON o.salesman_id = s.salesman_id
WHERE s.name = 'Paul Adam';
```

**Output:**


<img width="1036" height="367" alt="image" src="https://github.com/user-attachments/assets/cb77c562-b216-4792-b8fa-a32762e08eaa" />


**Question 5**

```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
1           Ramesh      32          Ahmedabad   2000
3           Kaushik     23          Kota        2000
4           Chaitali    25          Mumbai      6500
5           Hardik      27          Bhopal      8500
6           Komal       22          Hyderabad   4500
7           Muffy       24          Indore      10000




```

```sql
SELECT * 
FROM CUSTOMERS 
WHERE SALARY > 1500;
```

**Output:**


<img width="1005" height="518" alt="image" src="https://github.com/user-attachments/assets/7ffd3d4b-9196-4a3f-a31b-8066933a9474" />



**Question 6**
```
Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)



For example:

Result
medic  medication_name  dosage
-----  ---------------  ---------------
2      Ibuprofen        200mg


```

```sql
SELECT medication_id AS medic, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MIN(dosage)
    FROM Medications
);
```

**Output:**


<img width="767" height="367" alt="image" src="https://github.com/user-attachments/assets/37f8e8d5-c1e7-4b46-b85c-d1971899053b" />


**Question 7**
```

Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

For example:

Result
id     name             age              city             income
-----  ---------------  ---------------  ---------------  ----------
101    Peter            32               NewYork          200000
102    Mark             32               California       300000
103    Donald           25               Arizona          1000000
105    Linklon          32               Georgia          250000

```

```sql
SELECT *
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 1000000
);
```

**Output:**


<img width="1216" height="367" alt="image" src="https://github.com/user-attachments/assets/aba3777b-300e-403d-85a7-9831db7bf79f" />



**Question 8**
```

From the following tables, write a SQL query to determine the commission of the salespeople in Paris. Return commission.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
For example:

Result
commission
----------
0.14


```

```sql
SELECT commission
FROM salesman
WHERE salesman_id IN
    (SELECT salesman_id 
     FROM customer
     WHERE city = 'Paris');
```

**Output:**


<img width="352" height="326" alt="image" src="https://github.com/user-attachments/assets/b2c6de0b-1ebd-4f54-8f00-92767939e450" />


**Question 9**
```
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
name
---------------
Aarti Desai
Vivek Sharma
Nisha Patel
Rajesh Singh
Radha Iyer



```

```sql
SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(*) = 1
);
```

**Output:**



<img width="393" height="407" alt="image" src="https://github.com/user-attachments/assets/7ea6aa43-a5df-47db-8c09-3773eba58096" />


**Question 10**
```
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



For example:

Result
student_name     grade
---------------  ---------------
Bob              85
Frank            85
John             85


```

```sql
SELECT student_name, grade
FROM GRADES g
WHERE grade = (
    SELECT MIN(grade)
    FROM GRADES
    WHERE subject = g.subject
);
```

**Output:**


<img width="598" height="377" alt="image" src="https://github.com/user-attachments/assets/784fab59-f6bc-4dfb-963a-e3ea4bc234b6" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
