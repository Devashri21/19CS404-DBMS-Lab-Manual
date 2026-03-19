# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

```sql
UPDATE Products SET sell_price=sell_price*1.10
WHERE category='Bakery';
```

**Output:**

<img width="1173" height="503" alt="image" src="https://github.com/user-attachments/assets/dc652701-8ba1-4b19-9794-93faf481cd3a" />


**Question 2**
---
Write a SQL query to find customers who are either from the city 'New York' or who do not have a grade greater than 100. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002

```sql
SELECT customer_id,cust_name,city,grade,salesman_id
FROM customer
WHERE city='New York' OR grade<=100;
```

**Output:**

<img width="1171" height="401" alt="image" src="https://github.com/user-attachments/assets/7bcda66e-55d4-4c65-ab35-86e8b3c8087c" />


**Question 3**
---
Write a SQL query to Delete customers with following conditions

'CUST_COUNTRY' is not in a list of specified countries ('UK', 'USA', 'Canada')
'GRADE' is greater than or equal to 3

```sql
DELETE FROM Customer
WHERE cust_country NOT IN ('UK','USA','Canada') AND grade>=3
```

**Output:**

<img width="1176" height="404" alt="image" src="https://github.com/user-attachments/assets/e26ba483-15c8-439c-af24-346c67faa47c" />


**Question 4**
---
Write a SQL statement to Update the grade of all customers in Chennai city as  5. 

```sql
UPDATE Customer SET grade=5
WHERE city='Chennai';
```

**Output:**

<img width="1174" height="461" alt="image" src="https://github.com/user-attachments/assets/e5044590-b6d4-41d6-b73b-4e98275e20e5" />


**Question 5**
---
Write a query to calculate the discounted_price and  discounted_price_percentage for each product from the products table. Return product_id, original_price, discount_percentage, discounted_price, and discounted_price_percentage.

Discounted Price: Calculate the price of the product after applying the discount.

Discounted Price Percentage: Calculate the percentage that the discounted price represents relative to the original price.

```sql
SELECT product_id,original_price,discount_percentage,
original_price*(1-discount_percentage) AS discounted_price,
CAST((1-discount_percentage)*100 AS INT)||'%' AS discounted_price_percentage
FROM Products;
```

**Output:**

<img width="1174" height="290" alt="image" src="https://github.com/user-attachments/assets/67593ded-b34d-4faf-a6bf-d25e3e14fdfc" />


**Question 6**
---
Write a SQL query to Delete customers with 'GRADE' 3 or 'AGENT_CODE' 'A008' whose 'OUTSTANDING_AMT' is less than 5000

```sql
DELETE FROM Customer 
WHERE (grade=3 OR agent_code='A008') AND outstanding_amt<5000;
```

**Output:**

<img width="1175" height="374" alt="image" src="https://github.com/user-attachments/assets/22f1dc6a-42f1-4f88-b63b-05ff518cbec2" />


**Question 7**
---
Write a SQL query to Select all patients whose name starts with A.

```sql
SELECT patient_id,first_name,last_name,date_of_birth,admission_date,discharge_date,doctor_id
FROM Patients
WHERE first_name LIKE 'A%'
```

**Output:**

<img width="1174" height="333" alt="image" src="https://github.com/user-attachments/assets/883193d4-0f99-497d-ba5a-6355fcdc0e60" />


**Question 8**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' contains the substring 'Holmes'.

```sql
DELETE FROM Customer
WHERE cust_name LIKE '%Holmes%'
```

**Output:**

<img width="1176" height="531" alt="image" src="https://github.com/user-attachments/assets/67761b7d-47f6-4d08-a590-ae6c3859c8da" />


**Question 9**
---
Write a SQL query to assess the performance of value2 as 'Poor', 'Average', or 'Excellent' based on whether it is less than 30, between 30 and 70, or greater than 70 in the Calculations table

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0

```sql
SELECT id,value2,
    CASE
        WHEN value2<30 THEN 'Poor'
        WHEN value2 BETWEEN 30 AND 70 THEN 'Average'
        WHEN value2>70 THEN 'Excellent'
    END AS performance
FROM Calculations;
```

**Output:**

<img width="1166" height="416" alt="image" src="https://github.com/user-attachments/assets/0af24a2f-7325-42c5-98e2-cda172791298" />


**Question 10**
---
Write a SQL statement to Display the order number, orderdate and the purchase amount of
orders table which will be delivered by the salesman with ID 5001.

orders table

```sql
SELECT order_no,order_date,purch_amt
FROM orders
WHERE salesman_id=5001;
```

**Output:**

<img width="1168" height="387" alt="image" src="https://github.com/user-attachments/assets/3e2a6703-7b65-41b4-a110-d7d0778233eb" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
