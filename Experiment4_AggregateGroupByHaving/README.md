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
How many doctors specialize in each medical specialty?

Sample table:Doctors Table



For example:

Result
Specialty          TotalDocto
-----------------  ----------
Gastroenterology   1
Neurology          1
Obstetrics         3
Ophthalmology      1
Orthopedics        1
Pediatrics         2
Urology            1


```sql
SELECT 
    Specialty, 
    COUNT(*) AS TotalDoctors
FROM 
    Doctors
GROUP BY 
    Specialty;
```

**Output:**

<img width="848" height="639" alt="image" src="https://github.com/user-attachments/assets/d73d3942-3afb-47c4-a109-1788bea1134f" />


**Question 2**
---
What is the average age of doctors in each medical specialty?

Sample table:Doctors Table



For example:

Result
Specialty          AvgAge
-----------------  ----------
Endocrinology      44.0
Gastroenterology   39.0
Neurology          41.0
Obstetrics         53.0
Pediatrics         48.0
Urology            44.0

```sql
SELECT 
  Specialty,
  ROUND(AVG((julianday('now') - julianday(DateOfBirth)) / 365.25), 1) AS AvgAge
FROM Doctors
WHERE DateOfBirth IS NOT NULL
GROUP BY Specialty
ORDER BY Specialty;
```

**Output:**

<img width="922" height="716" alt="image" src="https://github.com/user-attachments/assets/056a2a65-7c2b-431d-af5b-39696e5e4024" />


**Question 3**
---
How many patients are there in each age group category (e.g., under 20, 20-30, 30-40, etc.)?

Sample table: Patients Table



For example:

Result
AgeGroup    TotalPatients
----------  -------------
20-30       1
31-40       5
41-50       3
Above 50    1

```sql
SELECT 
  CASE
    WHEN (strftime('%Y', 'now') - strftime('%Y', DateOfBirth)) < 20 THEN 'Under 20'
    WHEN (strftime('%Y', 'now') - strftime('%Y', DateOfBirth)) BETWEEN 20 AND 30 THEN '20-30'
    WHEN (strftime('%Y', 'now') - strftime('%Y', DateOfBirth)) BETWEEN 31 AND 40 THEN '31-40'
    WHEN (strftime('%Y', 'now') - strftime('%Y', DateOfBirth)) BETWEEN 41 AND 50 THEN '41-50'
    ELSE 'Above 50'
  END AS AgeGroup,
  COUNT(*) AS TotalPatients
FROM Patients
GROUP BY AgeGroup
ORDER BY AgeGroup;
```

**Output:**

<img width="743" height="524" alt="image" src="https://github.com/user-attachments/assets/bb3fcb43-bcde-4e30-b8d4-aca913eb4a2e" />


**Question 4**
---
Write a SQL query to find the youngest employee in the company?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
 

For example:

Result
Employee_Name  Age
-------------  ----------
Peter          32


```sql
SELECT name AS Employee_Name, age AS Age
FROM employee
ORDER BY age ASC
LIMIT 1;
```

**Output:**

<img width="710" height="363" alt="image" src="https://github.com/user-attachments/assets/08847276-9719-491a-a8c7-c275933000cf" />


**Question 5**
---
Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida.

Sample table: customer



 

For example:

Result
COUNT
----------
1


```sql
SELECT 
    COUNT(*) AS COUNT
FROM customer
WHERE city = 'Noida';
```

**Output:**

<img width="551" height="392" alt="image" src="https://github.com/user-attachments/assets/5b566753-c7ff-48cc-b84c-f8e1022aa4ef" />


**Question 6**
---
Write a SQL query to find the average length of names for people living in Chennai?

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
avg_name_length
---------------
10.0

```sql
SELECT AVG(LENGTH(name)) AS avg_name_length
FROM customer
WHERE city = 'Chennai';
```

**Output:**

<img width="653" height="421" alt="image" src="https://github.com/user-attachments/assets/1b6f79a1-c0e4-4fb7-964a-a31f8e03fc5c" />


**Question 7**
---
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

```sql
SELECT 
    name, 
    email, 
    LENGTH(email) AS min_email_length
FROM customer
ORDER BY LENGTH(email) ASC
LIMIT 1;
```

**Output:**

<img width="1109" height="409" alt="image" src="https://github.com/user-attachments/assets/3fc8c06a-c8f8-4dab-b77d-af0de009d967" />


**Question 8**
---
Write the SQL query that achieves the selection of category and calculates the sum of the product of price and category ID as Revenue for each category from the "products" table, and includes only those products where the total revenue is greater than 25.

Sample table: products



For example:

Result
category_id  Revenue
-----------  ----------
1            49.5
2            126
3            79.44

```sql
SELECT 
    category_id,
    SUM(price * category_id) AS Revenue
FROM products
GROUP BY category_id
HAVING SUM(price * category_id) > 25;
```

**Output:**

<img width="705" height="488" alt="image" src="https://github.com/user-attachments/assets/1d009d5f-1020-4f85-9c2e-2a15ecea8ca4" />


**Question 9**
---
Which cities (addresses) in the "customer1" table have an average salary lesser than Rs. 15000

Sample table: customer1



For example:

Result
address     AVG(salary)
----------  -----------
Ahmedabad   2000.0
Bhopal      8500.0
Delhi       1500.0
Hyderabad   4500.0
Indore      10000.0
Kota        2000.0
Mumbai      6500.0

```sql
SELECT 
    address,
    AVG(salary) AS "AVG(salary)"
FROM customer1
GROUP BY address
HAVING AVG(salary) < 15000;
```

**Output:**

<img width="695" height="601" alt="image" src="https://github.com/user-attachments/assets/aa2ed271-a21a-4a0a-a458-a35a6a7b7a40" />


**Question 10**
---
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 1,000,000.

Sample table: employee



For example:

Result
age         Income
----------  ----------
32          200000
40          350000
45          450000

```sql
SELECT 
    age,
    MIN(Income) AS Income
FROM employee
GROUP BY age
HAVING MIN(Income) < 1000000;
```

**Output:**

<img width="610" height="494" alt="image" src="https://github.com/user-attachments/assets/36ae0b88-c3f6-4b40-a8fc-3722ffbef106" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
