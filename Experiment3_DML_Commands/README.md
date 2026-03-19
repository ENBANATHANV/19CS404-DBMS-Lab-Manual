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
-- Write a SQL query to Delete All Doctors with a NULL Specialization
Sample table: Doctors
attributes : doctor_id, first_name, last_name, specialization

```sql
-- DELETE FROM Doctors
WHERE specialization IS NULL;
```

**Output:**

<img width="1231" height="916" alt="image" src="https://github.com/user-attachments/assets/306f701f-dc3c-433f-9341-7a5e83cc73e3" />


**Question 2**
---
--Write a SQL query to retrieve the details of all customers whose ID belongs to any of the values 3007, 3008 or 3009. Return customer_id, cust_name, city, grade, and salesman_id.

```sql
-- SELECT customer_id, cust_name, city, grade, salesman_id
FROM customer
WHERE customer_id IN (3007,3008,3009);
```

**Output:**

<img width="1144" height="332" alt="image" src="https://github.com/user-attachments/assets/50e784a3-1f5c-4062-b176-d7527569a1e1" />


**Question 3**
---
-- Write a query to find the names of employees that begin with ‘S’ from EmployeeInfo table.

```sql
-- select *
FROM EmployeeInfo 
WHERE EmpFname LIKE 'S%';
```

**Output:**

<img width="1292" height="152" alt="image" src="https://github.com/user-attachments/assets/43a6ff9f-7f12-4d0a-a19f-9aa3778ec1ef" />


**Question 4**
---
-- Write a SQL query to Delete customers with 'GRADE' 3 or 'AGENT_CODE' 'A008' whose 'OUTSTANDING_AMT' is less than 5000

```sql
-- DELETE FROM Customer
WHERE (GRADE = 3 OR AGENT_CODE = 'A008') AND OUTSTANDING_AMT <5000.00;
```

**Output:**

<img width="1038" height="112" alt="image" src="https://github.com/user-attachments/assets/c43953ed-f607-4e63-8104-b575bfcf84ab" />


**Question 5**
---
-- Write a SQL query to find the details of those salespeople who live in cities other than Paris and Rome. Return salesman_id, name, city, commission

```sql
-- SELECT *
FROM salesman
WHERE city NOT IN ('Paris' , 'Rome');
```

**Output:**

<img width="796" height="305" alt="image" src="https://github.com/user-attachments/assets/f3fa8161-507f-418f-b2fa-2db9ab553123" />


**Question 6**
---
-- Write a SQL query to calculate the discounted price for each product. Return product_id, original_price, discount_percentage, and discounted_price.

```sql
-- SELECT product_id, original_price, discount_percentage, original_price*(1-discount_percentage) AS discounted_price
FROM Products

```

**Output:**
<img width="1070" height="336" alt="image" src="https://github.com/user-attachments/assets/64be9c50-a59a-4299-86ea-e904446ffe1d" />


**Question 7**
---
-- Write a SQL query to Select all patients whose name starts with A.

```sql
-- SELECT *
FROM Patients
WHERE first_name  LIKE 'A%';7
```

**Output:**

<img width="1244" height="221" alt="image" src="https://github.com/user-attachments/assets/95647126-4d29-4120-9d92-11b6a311cb18" />


**Question 8**
---
-- Write a SQL query to Get the employee names where the first letter of each word is the same.

```sql
-- SELECT ename 
FROM emp
WHERE instr (ename, ' ')>0 AND substr(ename, 1,1) = substr(ename, instr(ename , ' ')+1 ,1);
```

**Output:**

<img width="276" height="261" alt="image" src="https://github.com/user-attachments/assets/e8851c9c-f5c9-49c6-8ac1-75333332d6ad" />


**Question 9**
---
-- Write a SQL statement to Increase quantity of all products by 10% to adjust for surplus stock counted

```sql
-- UPDATE Products 
SET quantity = quantity *(1.10);
```

**Output:**

<img width="1081" height="304" alt="image" src="https://github.com/user-attachments/assets/6c0df761-e721-487d-8f2b-2d102491014d" />


**Question 10**
---
-- Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the products table.

```sql
-- UPDATE Products 
SET reorder_lvl = reorder_lvl*(.70)
WHERE cost_price >50 AND quantity  <100;
```

**Output:**

<img width="1250" height="214" alt="image" src="https://github.com/user-attachments/assets/171ce441-6c2f-41c8-9b7d-a4527545065b" />
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/4a3395c4-6ff0-4689-a349-00e465b52674" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
