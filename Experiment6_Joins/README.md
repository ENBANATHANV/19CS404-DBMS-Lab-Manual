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
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for test results with a test date between '2024-03-01' and '2024-03-31'.

```sql
select p.*
from patients p
inner join TEST_RESULTS t on p.patient_id = t.patient_id
where test_date between '2024-03-01' and '2024-03-31';
```

**Output:**

<img width="1069" height="193" alt="image" src="https://github.com/user-attachments/assets/fc56c252-e5bc-473b-9f64-376ff368f76b" />


**Question 2**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name"), with an inner join on the "doctor_id" column and conditions filtering for patients whose doctor has the first name 'Emily', last name 'Johnson', and a non-null discharge date.

```sql
select p.first_name as patient_name
from PATIENTS  p
inner join DOCTORS d on p.doctor_id = d.doctor_id
where (d.first_name = 'Emily' AND d.last_name ='Johnson') and p.discharge_date not null;
```

**Output:**

<img width="207" height="196" alt="image" src="https://github.com/user-attachments/assets/8a97b70e-44a8-4dea-a2aa-22e154c15161" />


**Question 3**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with an order date between '2012-08-01' and '2012-08-30'.

```sql
-- select c.*
from CUSTOMER c
left join ORDERS  o on c.customer_id = o.customer_id
where ord_date BETWEEN '2012-08-01' and '2012-08-30';
```

**Output:**

<img width="790" height="236" alt="image" src="https://github.com/user-attachments/assets/35234b91-77d7-406c-8345-744c33c20cfe" />


**Question 4**
---
 Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

```sql
 select p.first_name as patient_name,t.*     
from PATIENTS p
inner join TEST_RESULTS t on p.patient_id = t.patient_id
where test_name = 'Blood Pressure';
```

**Output:**

<img width="892" height="198" alt="image" src="https://github.com/user-attachments/assets/0b6d138d-ca38-4857-a28f-ef9fcd0b9675" />


**Question 5**
---
Write the SQL query that accomplishes the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.


```sql
select p.first_name , c.*
from PATIENTS p
inner join SURGERIES  c on p.patient_id=c.patient_id
where p.first_name ='Alice';
```

**Output:**

<img width="797" height="197" alt="image" src="https://github.com/user-attachments/assets/2f15e7bf-8a99-4570-94cf-5787b1a01259" />


**Question 6**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "commission" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column.

```sql
select c.cust_name , s.commission
from Customer c
inner join Salesman  s on c.salesman_id=s.salesman_id;
```

**Output:**

<img width="372" height="451" alt="image" src="https://github.com/user-attachments/assets/861f89a3-3ffa-456b-981c-00e76e52db44" />


**Question 7**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

```sql
select s.name as Salesman,c.cust_name,c.city    
from salesman s
inner join customer c on s.city   = c.city   ;
```

**Output:**

<img width="518" height="346" alt="image" src="https://github.com/user-attachments/assets/3d1dd8a7-3e9e-4e27-b46d-3153df9d37d3" />


**Question 8**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with an order date later than '2012-08-17'.


```sql
select c.*
from CUSTOMER  c
left join ORDERS  o on c.customer_id =o.customer_id
where ord_date > '2012-08-17';
```

**Output:**

<img width="794" height="422" alt="image" src="https://github.com/user-attachments/assets/edf35d53-8336-4b84-8303-8c3ac67e9c9e" />


**Question 9**
---
Write the SQL query that accomplishes the selection of all columns from the "patients" table and the first name of doctors from the "doctors" table, with an inner join on the "doctor_id" column.

```sql
select p.*, d.first_name as doctor_name
from PATIENTS  p
inner join DOCTORS  d on p.doctor_id=d.doctor_id;
```

**Output:**

<img width="1187" height="272" alt="image" src="https://github.com/user-attachments/assets/0bf90dd3-1c7d-46c3-9e76-cff55bd71856" />


**Question 10**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'New York'.

```sql
select s.name as name 
from salesman s
left join Customer  c on c.salesman_id = s.salesman_id
where c.city = 'New York';
```

**Output:**

<img width="210" height="195" alt="image" src="https://github.com/user-attachments/assets/f7b8e682-a490-4146-a6e6-5119f3b7d246" />

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/cb0cfd6d-6771-474f-abcd-b0d46f41ad30" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
