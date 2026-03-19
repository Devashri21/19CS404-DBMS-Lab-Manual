# Experiment 4: Aggregate Functions, Group By and Having Clause

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
--
Write a SQL query to find the total number of unique cities in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER

```sql
SELECT COUNT(DISTINCT city) AS unique_cities
FROM customer;
```

**Output:**

<img width="1170" height="293" alt="image" src="https://github.com/user-attachments/assets/2ede1837-5d28-4af1-b004-5a0670b0288f" />


**Question 2**
---
Write a SQL query to find the difference between the maximum and minimum price of fruits?

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL

```sql
SELECT MAX(price)-MIN(price) AS price_diff
FROM fruits;
```

**Output:**

<img width="1172" height="295" alt="image" src="https://github.com/user-attachments/assets/4f8a2f2b-ad10-4b8b-9b08-2de2b9195e6c" />


**Question 3**
---
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
SELECT AVG(income) AS avg_income
FROM employee
WHERE name LIKE 'A%';
```

**Output:**

<img width="1173" height="291" alt="image" src="https://github.com/user-attachments/assets/d8d47dd1-9c47-4983-ac1d-80b7c31f9cc0" />


**Question 4**
---
How many appointments are scheduled for each doctor?

```sql
SELECT DoctorID, COUNT(AppointmentID) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID;
```

**Output:**

<img width="1171" height="612" alt="image" src="https://github.com/user-attachments/assets/e5970c35-fbf5-4cac-a0dd-b09b5cbfbc74" />


**Question 5**
---
How many prescriptions were written in each frequency category (e.g., once daily, twice daily)?

```sql
SELECT Frequency, COUNT(PrescriptionID) AS TotalPrescriptions
FROM Prescriptions
GROUP BY Frequency;
```

**Output:**

<img width="1170" height="514" alt="image" src="https://github.com/user-attachments/assets/fe7b735f-dfa2-4eba-99fd-cfc5c8741129" />


**Question 6**
---
How many patients are there in each city?

```sql
SELECT Address, COUNT(PatientID) AS TotalPatients
FROM Patients
GROUP BY Address;
```

**Output:**

<img width="1164" height="388" alt="image" src="https://github.com/user-attachments/assets/bfa80926-6c93-45aa-8793-5838ada1b94f" />


**Question 7**
---
Write a SQL query to identify the cities (addresses) where the average salary is greater than Rs. 5000, as per the "customer1" table.

```sql
SELECT address, AVG(salary) AS "AVG(salary)"
FROM customer1
GROUP BY address
HAVING AVG(salary)>5000;
```

**Output:**

<img width="1175" height="417" alt="image" src="https://github.com/user-attachments/assets/114d9cfd-0a35-4033-abae-0979a8c18a20" />


**Question 8**
---
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

```sql
SELECT address, SUM(salary) AS "SUM(salary)"
FROM customer1
GROUP BY address
HAVING SUM(salary)>2000;
```

**Output:**

<img width="1167" height="462" alt="image" src="https://github.com/user-attachments/assets/6fe730cf-b583-4438-a057-b8b5475267dd" />


**Question 9**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the total salary sum for each group, and excludes groups where the total salary sum is not greater than 5000.

```sql
SELECT (age/5)*5 AS age_group, SUM(salary)
FROM customer1
GROUP BY age_group
HAVING SUM(salary)>5000;
```

**Output:**

<img width="1173" height="346" alt="image" src="https://github.com/user-attachments/assets/596b77e8-16de-4c0c-9086-17369fabbe40" />


**Question 10**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the total work hours for each date, and excludes dates where the total work hour sum is not greater than 40.

```sql
SELECT jdate, SUM(workhour)
FROM employee1
GROUP BY jdate
HAVING SUM(workhour)>40;
```

**Output:**

<img width="1175" height="365" alt="image" src="https://github.com/user-attachments/assets/a4538c98-eb81-4880-8d51-6e6ce14f9165" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
