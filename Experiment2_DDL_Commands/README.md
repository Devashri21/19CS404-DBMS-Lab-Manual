# Experiment 2: DDL Commands

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
--
```
Create a table named Locations with the following columns:

LocationID as INTEGER
LocationName as TEXT
Address as TEXT
For example:

Test	Result
pragma table_info('Locations');
cid       name             type        notnull     dflt_value  pk
--------  ---------------  ----------  ----------  ----------  ----------
0         LocationID       INTEGER     0                       0
1         LocationName     TEXT        0                       0
2         Address          TEXT        0                       0
```

```sql
CREATE TABLE Locations
(
    LocationID INTEGER,
    LocationName TEXT,
    Address TEXT
);
```

**Output:**

<img width="1177" height="365" alt="image" src="https://github.com/user-attachments/assets/93c552ec-9be9-40e3-89c2-5249da202575" />


**Question 2**
---
```
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

For example:

Test	Result
select * from Customers;
CustomerID  Name             Address         Email
----------  ---------------  --------------  ---------------------
301         Michael Johnson  123 Elm Street  michael.j@example.com
302         Sarah Lee        456 Oak Avenue  sarah.lee@example.com
303         David Wilson     789 Pine Road   david.w@example.com

```

```sql
INSERT INTO Customers('CustomerID', 'Name', 'Address', 'Email')
SELECT CustomerID, Name, Address, Email FROM Old_customers;
```

**Output:**

<img width="1177" height="276" alt="image" src="https://github.com/user-attachments/assets/c2701727-5d4d-4341-9283-9192824ca358" />


**Question 3**
---
```
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

For example:
Test:
INSERT INTO Attendance (AttendanceID, EmployeeID, AttendanceDate, Status) VALUES (1, 1, '2024-08-01', 'Present');
SELECT * FROM Attendance;
Result:
AttendanceID  EmployeeID  AttendanceDate  Status
------------  ----------  --------------  ----------
1             1           2024-08-01      Present
```

```sql
CREATE TABLE Attendance
(
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE NOT NULL,
    Status TEXT,
    FOREIGN KEY(EmployeeID)
        REFERENCES Employees(EmployeeID),
    CHECK(Status IN('Present','Absent','Leave'))
);
```

**Output:**

<img width="1170" height="268" alt="image" src="https://github.com/user-attachments/assets/0c0dc012-1a28-4d20-af9a-72a91a67561a" />


**Question 4**
---
```
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

For example:
Test:
INSERT INTO Customers (CustomerID, FirstName, LastName, Email) VALUES (1, 'Alice', 'Johnson', 'alice.johnson@example.com');
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
select * from orders;
Result:
OrderID     OrderDate   CustomerID
----------  ----------  ----------
1           2024-08-01  1

```

```sql
CREATE TABLE Orders
(
    OrderID INTEGER PRIMARY KEY,
    OrderDate DATE NOT NULL,
    CustomerID INTEGER,
    FOREIGN KEY(CustomerID)
        REFERENCES Customers(CustomerID)
);
```

**Output:**

<img width="1173" height="270" alt="image" src="https://github.com/user-attachments/assets/74c2b208-4b84-4ac7-b086-bafecfe6b3fe" />


**Question 5**
---
```
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.

For example:
Test:
-- Attempt to insert a record with NULL FirstName
INSERT INTO Employees (EmployeeID, FirstName, LastName, Email, Salary, DepartmentID)
VALUES (1, NULL, 'Doe', 'john.doe@example.com', 50000, 1);
Result:
Error: NOT NULL constraint failed: Employees.FirstName
```

```sql
CREATE TABLE Employees
(
    EmployeeID INTEGER PRIMARY KEY,
    FirstName TEXT NOT NULL,
    LastName TEXT NOT NULL,
    Email TEXT NOT NULL UNIQUE,
    Salary INTEGER NOT NULL,
    DepartmentID INTEGER,
    FOREIGN KEY(DepartmentID)
        REFERENCES Departments(DepartmentID)
    CHECK(Salary>0)
);
```

**Output:**

<img width="1172" height="401" alt="image" src="https://github.com/user-attachments/assets/c43c7e82-b4b9-4d48-bad7-22a47f864283" />


**Question 6**
---
```
Write an SQL command can to add a column named email of type TEXT to the customers table

For example:

Test:
pragma table_info('Customers');
Result:
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           name        text        0                       0
2           email       TEXT        0                       0

```

```sql
ALTER TABLE Customers
ADD COLUMN email TEXT;
```

**Output:**

<img width="1169" height="268" alt="image" src="https://github.com/user-attachments/assets/4893db01-8ec3-4c0b-8bf5-1b77d45ef186" />


**Question 7**
---
```
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100
 
For example:
Test:
SELECT * FROM Products;
Result:
ProductID   Name             Category    Price       Stock
----------  ---------------  ----------  ----------  ----------
106         Fitness Tracker  Wearables
107         Laptop           Electronic  999.99      50
108         Wireless Earbud  Accessorie              100

```

```sql
INSERT INTO Products('ProductID', 'Name', 'Category', 'Price', 'Stock')
VALUES (106,'Fitness Tracker','Wearables',NULL,NULL);
INSERT INTO Products('ProductID', 'Name', 'Category', 'Price', 'Stock')
VALUES (107,'Laptop','Electronics',999.99,50);
INSERT INTO Products('ProductID', 'Name', 'Category', 'Price', 'Stock')
VALUES (108,'Wireless Earbuds','Accessorie',NULL,100);
```

**Output:**

<img width="1174" height="266" alt="image" src="https://github.com/user-attachments/assets/249b25c7-7726-4c63-b818-8f05789dcff9" />


**Question 8**
---
```
Write a SQL query to Rename the "city" column to "location" in the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
```

```sql
ALTER TABLE customer
RENAME COLUMN city TO location;
```

**Output:**

<img width="1173" height="320" alt="image" src="https://github.com/user-attachments/assets/6c454a69-5fac-4f3d-b47c-8d06bdc3a8e5" />


**Question 9**
---
```
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.
```

```sql
CREATE TABLE jobs
(
    job_id INTEGER PRIMARY KEY,
    job_title VARCHAR(50) DEFAULT '',
    min_salary INT DEFAULT 8000,
    max_salary INT DEFAULT NULL
);
```

**Output:**

<img width="1169" height="311" alt="image" src="https://github.com/user-attachments/assets/d0523950-3b22-4b10-9c57-0413e24e5633" />


**Question 10**
---
```
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.
```

```sql
INSERT INTO Products
VALUES (104,'Tablet','Electronics',100,50)
```

**Output:**

<img width="1173" height="212" alt="image" src="https://github.com/user-attachments/assets/146efe56-955c-40fc-8a24-7c650cad4013" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
