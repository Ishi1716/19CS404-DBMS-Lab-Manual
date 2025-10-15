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
 Update the total selling price to quantity sold multiplied by updated selling price per unit where product id is 10 in the sales table.

SALES TABLE
name               type
-----------------  ---------------
sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)
For example:

Test	Result
select changes();
changes()
----------
3


```sql

UPDATE sales
SET total_sell_price = quantity * sell_price
WHERE product_id = 10;


```

**Output:**

<img width="1297" height="401" alt="image" src="https://github.com/user-attachments/assets/483900f3-3155-43bd-ad1e-a6be09822061" />


**Question 2**
---

Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the products table.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT               
For example:

Test	Result
--pragma table_info('products');
select changes();
changes()
----------
2

```sql

UPDATE products
SET reorder_lvl = CAST(reorder_lvl * 0.7 AS INT)
WHERE cost_price > 50
  AND quantity < 100;
```

**Output:**

<img width="1341" height="367" alt="image" src="https://github.com/user-attachments/assets/04b33365-d577-4930-9a56-1f9a3d9278ef" />


**Question 3**
---

Write a SQL statement to change the first_name column of employees table with 'John' for those employees whose department_id is 80 and gets a commission_pct below 0.35.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT * FROM EMPLOYEES WHERE DEPARTMENT_ID=80 AND COMMISSION_PCT=.25;
EMPLOYEE_ID  FIRST_NAME  LAST_NAME   EMAIL       PHONE_NUMBER        HIRE_DATE   JOB_ID      SALARY      COMMISSION_PCT  MANAGER_ID  DEPARTMENT_ID
-----------  ----------  ----------  ----------  ------------------  ----------  ----------  ----------  --------------  ----------  -------------
151          John        Bernstein   DBERNSTE    011.44.1344.345268  8/7/87      SA_REP      9500        0.25            145         80
152          John        Hall        PHALL       011.44.1344.478968  8/8/87      SA_REP      9000        0.25            145         80
161          John        Sewall      SSEWALL     011.44.1345.529268  8/17/87     SA_REP      7000        0.25            146         80
162          John        Vishney     CVISHNEY    011.44.1346.129268  8/18/87     SA_REP      10500       0.25            147         80
168          John        Ozer        LOZER       011.44.1343.929268  8/24/87     SA_REP      11500       0.25            148         80
175          John        Hutton      AHUTTON     011.44.1644.429266  8/31/87     SA_REP      8800        0.25            149         80


```sql

UPDATE employees
SET first_name = 'John'
WHERE department_id = 80
  AND commission_pct < 0.35;
```

**Output:**

<img width="1328" height="409" alt="image" src="https://github.com/user-attachments/assets/11fac1af-478c-4fc6-ae61-dd45603c9f32" />


**Question 4**
---
Change the supplier name to upper case where contact person contains ' Singh' in suppliers table.

name               type
-----------------  ---------------
supplier_id        INT
supplier_name      VARCHAR(100)
contact_person     VARCHAR(100)
phone_number       VARCHAR(20)
email              VARCHAR(100)
address            VARCHAR(250)
For example:

Test	Result
select changes();
changes()
-----------------
2


```sql

UPDATE suppliers
SET supplier_name = UPPER(supplier_name)
WHERE contact_person LIKE '% Singh';

```

**Output:**

<img width="1362" height="278" alt="image" src="https://github.com/user-attachments/assets/fc4cb5ed-fac1-4394-a1f6-e0d614cfc7c4" />



**Question 5**
---
Write a SQL statement to change the email column of employees table with 'Unavailable' for all employees in employees table.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
 

For example:

Test	Result
SELECT EMPLOYEE_ID,FIRST_NAME,EMAIL FROM EMPLOYEES LIMIT 2;
EMPLOYEE_ID  FIRST_NAME  EMAIL
-----------  ----------  -----------
100          Steven      Unavailable
101          Neena       Unavailable


```sql

UPDATE employees
SET email = 'Unavailable';
```

**Output:**

<img width="1048" height="326" alt="image" src="https://github.com/user-attachments/assets/fd8d404c-aa71-463a-b3a7-12844835d6ae" />


**Question 6**
---
Write a SQL query to delete a doctor from Doctors table whos specialization is 'Cardiology'

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM doctors
WHERE specialization = 'Cardiology';

```

**Output:**

<img width="996" height="284" alt="image" src="https://github.com/user-attachments/assets/d906422a-cccf-467f-b088-a4e872d4bece" />


**Question 7**
---
Write a SQL query to remove rows from the table 'customer' with the following condition -

1. 'cust_city' should begin with the letter 'L',

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
SELECT * FROM customer WHERE cust_country='UK';
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00013      Holmes      London      London        UK            2           6000         5000         7000         4000             BBBBBBB     A003
C00024      Cook        London      London        UK            2           4000         9000         7000         6000             FSDDSDF     A006
C00015      Stuart      London      London        UK            1           6000         8000         3000         11000            GFSGERS     A003
C00023      Karl        London      London        UK            0           4000         6000         7000         3000             AAAABAA     A006
C00010      Charles     Hampshair   Hampshair     UK            3           6000         4000         5000         5000             MMMMMMM     A009
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00010      Charles     Hampshair   Hampshair     UK            3           6000         4000         5000         5000             MMMMMMM     A

```sql
DELETE FROM customer
WHERE cust_city LIKE 'L%';

```

**Output:**

<img width="1377" height="591" alt="image" src="https://github.com/user-attachments/assets/dcf65381-882c-48f6-9c9c-209157061446" />


**Question 8**
---
Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM doctors
WHERE specialization = 'Pediatrics'
  AND first_name = 'Michael';
```

**Output:**

<img width="1025" height="284" alt="image" src="https://github.com/user-attachments/assets/196629f6-3946-4d1a-b6fc-476a7ff90442" />


**Question 9**
---
Write a SQL query to Delete All Doctors with a NULL Specialization

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
4           Febin       Jones
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics


```sql
DELETE FROM doctors
WHERE specialization IS NULL;

```

**Output:**

<img width="1091" height="767" alt="image" src="https://github.com/user-attachments/assets/65d86df3-2558-4a0d-90a8-a19970062119" />


**Question 10**
---
Write a SQL query to Delete a Specific Surgery whose ID is 3

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date
For example:

Test	Result
SELECT * FROM surgeries;
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
3           3           3           2024-03-25
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28

```sql
DELETE FROM surgeries
WHERE surgery_id = 3;

```

**Output:**

<img width="992" height="281" alt="image" src="https://github.com/user-attachments/assets/c478b57a-9952-4997-949e-bf2355fdca71" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
