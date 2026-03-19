# Experiment 5: Subqueries and Views

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
--
Write a SQL query to List departments with names longer than the average length

```sql
SELECT department_id AS depar, department_name
FROM Departments
WHERE LENGTH(department_name)>(
    SELECT AVG(LENGTH(department_name))
    FROM Departments
);
```

**Output:**

<img width="1172" height="384" alt="image" src="https://github.com/user-attachments/assets/6f9b6852-74bc-42e6-b9f9-008080f9802c" />


**Question 2**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than $30

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


```sql
SELECT *
FROM CUSTOMERS
WHERE AGE<30;
```

**Output:**

<img width="1166" height="561" alt="image" src="https://github.com/user-attachments/assets/284dc767-ebbb-4b05-a50e-77853a70fae8" />


**Question 3**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table:

name             type
------------   ---------------
id                    INTEGER
name              TEXT
age                 INTEGER
city                 TEXT
income           INTEGER

```sql
SELECT id, name, age, city, income
FROM Employee
WHERE age<(
    SELECT AVG(age)
    FROM Employee
    WHERE income>250000
);
```

**Output:**

<img width="1172" height="510" alt="image" src="https://github.com/user-attachments/assets/91da6453-70dd-45b9-9fc1-2a967d900444" />


**Question 4**
---
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
SELECT id, name, city, email, phone
FROM customer
WHERE city!=(
    SELECT city
    FROM customer
    WHERE id=(SELECT MAX(id) FROM customer )
);
```

**Output:**

<img width="1170" height="481" alt="image" src="https://github.com/user-attachments/assets/dd9c2701-9fe3-4a4c-aed3-ffdab6a66ffd" />


**Question 5**
---
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format

ORDERS TABLE

name            type
----------     ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM ORDERS
WHERE purch_amt>(
    SELECT AVG(purch_amt)
    FROM ORDERS
    WHERE ord_date='2012-10-10'
);
```

**Output:**

<img width="1173" height="459" alt="image" src="https://github.com/user-attachments/assets/2a66beb0-e9bf-41ac-b0ee-389a1f791395" />


**Question 6**
---
From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

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

```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.salesman_id
FROM orders o
JOIN salesman s ON o.salesman_id = s.salesman_id
WHERE s.commission=(
    SELECT MAX(commission)
    FROM salesman
);
```

**Output:**

<img width="1175" height="456" alt="image" src="https://github.com/user-attachments/assets/7e566ed8-a335-4ce3-939b-10db1b67cacb" />


**Question 7**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
SELECT name, city
FROM customer
WHERE city IN(
    SELECT city
    FROM customer
    WHERE id IN (3,7)
);
```

**Output:**

<img width="1171" height="446" alt="image" src="https://github.com/user-attachments/assets/9aaec198-cd8e-4751-880f-1ae9540e4ab1" />


**Question 8**
---
From the following tables, write a SQL query to find all orders generated by the salespeople who may work for customers whose id is 3007. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

```sql
SELECT *
FROM Orders
WHERE salesman_id IN(
    SELECT salesman_id
    FROM Orders
    WHERE customer_id=3007
);
```

**Output:**

<img width="1170" height="433" alt="image" src="https://github.com/user-attachments/assets/bc4d5cf5-bf34-4cd1-9279-f45e47605393" />


**Question 9**
---
From the following tables write a SQL query to find all orders generated by New York-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM Orders o
JOIN Salesman s ON o.salesman_id = s.salesman_id
WHERE s.city='New York';
```

**Output:**

<img width="1174" height="462" alt="image" src="https://github.com/user-attachments/assets/4ce70048-ab72-4b08-be39-cddb24dd23de" />


**Question 10**
---
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

```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY>1500;
```

**Output:**

<img width="1173" height="605" alt="image" src="https://github.com/user-attachments/assets/efa2821b-8d68-4508-88a4-f5a38c81e9ce" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
