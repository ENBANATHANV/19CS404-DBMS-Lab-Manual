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
-- Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```sql
-- CREATE TABLE contacts (
contact_id int PRIMARY KEY,
first_name text NOT NULL,
last_name text NOT NULL,
email text,
phone text NOT NULL CHECK (length(phone)>=10)
);
```

**Output:**

<img width="1349" height="151" alt="image" src="https://github.com/user-attachments/assets/a04dd9d0-8504-468c-ab85-6283fc40960d" />


**Question 2**
---
-- Insert all employees from Former_employees into Employee
Table attributes are EmployeeID, Name, Department, Salary

```sql
-- INSERT INTO Employee
SELECT EmployeeID, Name, Department, Salary
FROM Former_employees ;
```

**Output:**

<img width="1079" height="226" alt="image" src="https://github.com/user-attachments/assets/09f9f703-71e9-462a-be78-2696379f0b94" />

**Question 3**
---
-- Write a SQL Query  to Rename attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date,State as varchar(30) in the table Companies. 

```sql
-- ALTER TABLE Companies
RENAME COLUMN name TO first_name;
ALTER TABLE Companies
ADD COLUMN mobilenumber number;
ALTER TABLE Companies
ADD COLUMN DOB Date;
ALTER TABLE Companies
ADD COLUMN State varchar(30)
```

**Output:**

<img width="1267" height="314" alt="image" src="https://github.com/user-attachments/assets/7c3a6080-7cc8-4aa5-9114-fd80476b5894" />


**Question 4**
---
-- Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.

```sql
-- CREATE TABLE Department (
DepartmentID int PRIMARY KEY,
DepartmentName text UNIQUE NOT NULL,
Location text
);
```

**Output:**

<img width="1210" height="125" alt="image" src="https://github.com/user-attachments/assets/3a68e597-af90-4d8a-963e-7f49af8e4a85" />


**Question 5**
---
-- Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
-- CREATE TABLE Invoices (
InvoiceID int PRIMARY KEY,
InvoiceDate DATE,
Amount REAL CHECK (Amount > 0),
DueDate REAL CHECK (InvoiceDate < DueDate),
OrderID int ,
FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1165" height="130" alt="image" src="https://github.com/user-attachments/assets/08df4794-c723-492b-8b6c-e43ee0260115" />


**Question 6**
---
-- Create a table named Customers with the following columns:
CustomerID as INTEGER
Name as TEXT
Email as TEXT
JoinDate as DATETIME

```sql
--CREATE TABLE Customers (
CustomerID INTEGER,
Name TEXT,
Email TEXT,
JoinDate DATETIME 
);
```

**Output:**

<img width="1070" height="190" alt="image" src="https://github.com/user-attachments/assets/9bdd5d34-6e61-44f8-be8f-76704cd5b133" />


**Question 7**
---
-- Create a table named Departments with the following columns:
DepartmentID as INTEGER
DepartmentName as TEXT

```sql
-- CREATE TABLE Departments (
DepartmentID  INTEGER,
DepartmentName  TEXT
);
```

**Output:**

<img width="883" height="162" alt="image" src="https://github.com/user-attachments/assets/b4c462d9-635a-4640-8d10-48a2894fcdde" />


**Question 8**
---
-- Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

```sql
-- INSERT INTO Student_details (RollNo,Name ,Gender)
VALUES (204,'Samuel Black' ,'M')
```

**Output:**

<img width="580" height="147" alt="image" src="https://github.com/user-attachments/assets/0979616d-a211-4aed-8660-cdca54551804" />


**Question 9**
---
-- Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details tab

```sql
-- ALTER TABLE Student_details  
ADD COLUMN MobileNumber NUMBER;
ALTER TABLE Student_details  
ADD COLUMN Address VARCHAR(100);
```

**Output:**

<img width="876" height="181" alt="image" src="https://github.com/user-attachments/assets/7fb1b01f-4f8f-436b-9a98-e33fcee7bec0" />


**Question 10**
---
-- nsert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

```sql
-- INSERT INTO Customers 
VALUES(301,'Michael Jordan','123 Maple St','Chicago',60616)
```

**Output:**

<img width="872" height="103" alt="image" src="https://github.com/user-attachments/assets/3723aeaa-5bd8-433f-9d77-6bd7695cf911" />

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/bba1719d-91e9-4654-ac3a-a6763049dd60" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
