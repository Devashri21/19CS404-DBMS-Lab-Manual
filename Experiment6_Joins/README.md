# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and conditions filtering for test results with the test names 'Blood Test' or 'Blood Pressure' and results not containing the substring 'Normal'.

```sql
SELECT p.*
FROM patients p
INNER JOIN test_results t ON P.patient_id = t.patient_id
WHERE t.test_name='Blood Pressure';
```

**Output:**

<img width="1169" height="405" alt="image" src="https://github.com/user-attachments/assets/ea14fb3e-a9c6-4829-afc9-53482c4afd9d" />


**Question 2**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the same city as the salesman.

```sql
SELECT c.cust_name, s.name
FROM customer c
LEFT JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE s.city=c.city;
```

**Output:**

<img width="1170" height="526" alt="image" src="https://github.com/user-attachments/assets/fa10774d-1f77-4d96-9543-8a80c50807c2" />


**Question 3**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  


```sql
SELECT c.cust_name, c.city, c.grade, s.name AS Salesman, s.city
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;
```

**Output:**

<img width="1176" height="313" alt="image" src="https://github.com/user-attachments/assets/24999264-e420-4244-9b9d-81ba32843daf" />


**Question 4**
---
Write the SQL query that accomplishes the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.


```sql
SELECT p.first_name,s.*
FROM patients p
INNER JOIN surgeries s ON p.patient_id = s.patient_id
WHERE p.first_name='Alice';
```

**Output:**

<img width="1170" height="403" alt="image" src="https://github.com/user-attachments/assets/6795ab95-a7b6-4af1-851c-067dda8a0993" />


**Question 5**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the specialization from the "doctors" table (aliased as "Doctor_specialization"), with an inner join on the "doctor_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.

```sql
SELECT p.first_name AS patient_name, d.specialization AS Doctor_speciali
FROM patients p
INNER JOIN doctors d ON p.doctor_id = d.doctor_id
WHERE admission_date BETWEEN '2024-01-01' AND '2024-01-31';
```

**Output:**

<img width="1172" height="384" alt="image" src="https://github.com/user-attachments/assets/804ea1fb-35c8-4a41-92e9-b8084e34e3d9" />


**Question 6**
---
Write the SQL query that accomplishes the selection of the first name and last name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date between '2024-01-01' and '2024-01-31'.

```sql
SELECT p.first_name, p.last_name
FROM patients p
INNER JOIN surgeries s ON p.patient_id = s.patient_id
WHERE s.surgery_date BETWEEN '2024-01-01' AND '2024-01-31';
```

**Output:**

<img width="1173" height="381" alt="image" src="https://github.com/user-attachments/assets/0d736587-f2e2-4090-a3b5-70a82d45def5" />


**Question 7**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "commission" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column.

```sql
SELECT c.cust_name, s.commission
FROM customer c
LEFT JOIN salesman s ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="1169" height="311" alt="image" src="https://github.com/user-attachments/assets/ef3512ee-9d56-4dee-b43c-d363696f0ef1" />


**Question 8**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), with a left join on the "customer_id" column.

```sql
SELECT c.cust_name
FROM customer c
LEFT JOIN orders o on c.customer_id = o.customer_id;
```

**Output:**

<img width="1164" height="413" alt="image" src="https://github.com/user-attachments/assets/0d4e79ab-9fc0-48d3-8cc5-590cce2483ec" />


**Question 9**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name"), with an inner join on the "doctor_id" column and conditions filtering for patients whose doctor has the first name 'Emily', last name 'Johnson', and a non-null discharge date.

```sql
SELECT p.first_name AS patient_name
FROM patients p
INNER JOIN doctors d ON p.doctor_id = d.doctor_id
WHERE d.first_name='Emily' AND d.last_name='Johnson';
```

**Output:**

<img width="1175" height="383" alt="image" src="https://github.com/user-attachments/assets/32ba0bd3-ac9c-49f8-90cc-94bd1f941160" />


**Question 10**
---
Write the SQL query that achieves the selection of all columns from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers with the name 'Fabian Johns'.

Customer Table:

```sql
SELECT s.*
FROM Salesman s
LEFT JOIN Customer c ON s.salesman_id = c.salesman_id
WHERE c.cust_name='Fabian Johns';
```

**Output:**

<img width="1170" height="400" alt="image" src="https://github.com/user-attachments/assets/2b078004-233c-42fa-8775-59b9da2b4dda" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
