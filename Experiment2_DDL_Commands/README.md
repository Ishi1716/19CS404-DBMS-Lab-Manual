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
In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021


``
## SQL

insert into books (ISBN,Title,Author,Publisher,Year) values ('978-1234567890','Introduction to AI','John Doe',Null,null);
insert into books (ISBN,Title,Author,Publisher,Year) values ('978-9876543210','Deep Learning','Jane Doe','TechPress','2022');
insert into books (ISBN,Title,Author,Publisher,Year) values ('978-1122334455','Cybersecurity Essentials','Alice Smith',null,'2021');

``

**Output:**

<img width="1286" height="375" alt="image" src="https://github.com/user-attachments/assets/3dbb3f71-8ec8-4692-a64e-fb1c21f0b293" />


**Question 2**
---
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.

For example:

Test	Result
SELECT ProductID, Name, Category, Price, Stock 
FROM Products 
WHERE ProductID = 104;
ProductID   Name        Category     Price       Stock
----------  ----------  -----------  ----------  ----------
104         Tablet      Electronics  100         50

`` 
## SQL

insert into products (ProductID,Name,Category,Price,Stock) values (104, 'Tablet' ,'Electronics',100,50);

``

**Output:**

<img width="1264" height="294" alt="image" src="https://github.com/user-attachments/assets/0ac2339f-510c-4d58-8996-adbfaa98c446" />


**Question 3**
---

Create a new table named products with the following specifications:

product_id as INTEGER and primary key.

product_name as TEXT and not NULL.

list_price as DECIMAL (10, 2) and not NULL.

discount as DECIMAL (10, 2) with a default value of 0 and not NULL.

A CHECK constraint at the table level to ensure:

list_price is greater than or equal to discount

discount is greater than or equal to 0

list_price is greater than or equal to 0

``

## SQL

create table products (
    product_id  integer primary key,
    product_name text not null,
    list_price DECIMAL (10, 2) not NULL check (list_price>= discount),
    discount DECIMAL (10, 2) default '0' not NULL check (discount >= 0)
    check (list_price >= 0)
);

``

**Output:**

<img width="1268" height="359" alt="image" src="https://github.com/user-attachments/assets/7d151675-86a8-400d-9a6e-0ee697de13bf" />


**Question 4**
---

Write an SQL query to add a new column email of type TEXT to the Student_details table, and ensure that this column cannot contain NULL values and make default value as 'Invalid'

For example:

Test	Result
INSERT INTO Student_details (RollNo, Name, Gender, Subject, email) 
VALUES (1, 'John Doe', 'M', 'Math', 'john@example.com');
select * from Student_details;
RollN  Name   Gen  Subject     email
-----  -----  ---  ----------  ----------------
1      John   M    Math        john@example.com


``
## SQL

alter table Student_details 
add column email TEXT not null default 'Invalid';

``

**Output:**

<img width="1322" height="343" alt="image" src="https://github.com/user-attachments/assets/ac92e6db-c047-4fb2-911a-3233a19a2440" />


**Question 5**
---
Create a table named Customers with the following columns:

CustomerID as INTEGER
Name as TEXT
Email as TEXT
JoinDate as DATETIME
For example:

Test	Result
pragma table_info('Customers');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           CustomerID  INTEGER     0                       0
1           Name        TEXT        0                       0
2           Email       TEXT        0                       0
3           JoinDate    DATETIME    0                       0



``
## SQL

create table Customers (
CustomerID INTEGER,
Name  TEXT,
Email TEXT,
JoinDate DATETIME
);

``

**Output:**

<img width="1264" height="404" alt="image" src="https://github.com/user-attachments/assets/d4449200-dc93-4c47-bf1c-2e7728f25191" />


**Question 6**
---
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

For example:

Test	Result
select * from Products;
ProductID   ProductName     Price       Stock
----------  --------------  ----------  ----------
101         Old Smartphone  199.99      0
102         Vintage Laptop  399.99      10
103         Classic Tablet  149.99      5


``

## SQL

insert into products select * from Discontinued_products;

``

**Output:**

<img width="1268" height="277" alt="image" src="https://github.com/user-attachments/assets/2269adcc-04ae-42eb-95a9-f88720e4be9a" />


**Question 7**
---
Write an SQL query to add two new columns, department_id and manager_id, to the table employee with datatype of INTEGER. The manager_id column should have a default value of NULL.

For example:

Test	Result
PRAGMA table_info(employee);
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           department  INTEGER     0                       0
3           manager_id  INTEGER     0           NULL        0

## SQL

alter table employee 
add column department_id INTEGER;

alter table employee
add column manager_id INTEGER default NULL;

**Output:**

<img width="1254" height="316" alt="image" src="https://github.com/user-attachments/assets/39fd095a-d594-42cb-85ef-81ed7819ade9" />


**Question 8**
---
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


## SQL

create table Products (
ProductID primary key,
ProductName NOT NULL,
Price real check (Price>0),
Stock integer check (Stock > 0)
);

**Output:**

<img width="1276" height="286" alt="image" src="https://github.com/user-attachments/assets/42e2ef4c-3743-4519-829d-875277610393" />


**Question 9**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

## SQL

create table Orders (
OrderID INTEGER primary key,
OrderDate DATE not NULL,
CustomerID INTEGER,
foreign key (CustomerID) references Customers(CustomerID)
);

**Output:**

<img width="1249" height="277" alt="image" src="https://github.com/user-attachments/assets/4e37162a-aed7-4bbc-8155-967a39760946" />

**Question 10**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.


## SQL 

create table item (
item_id TEXT primary key,
item_desc TEXT not NULL,
rate INTEGER not NULL,
icom_id TEXT (4),
foreign key (icom_id) references company(com_id)
on update cascade 
on delete cascade
);


**Output:**

<img width="1262" height="356" alt="image" src="https://github.com/user-attachments/assets/69191682-2965-426f-984e-fc06be83a529" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
