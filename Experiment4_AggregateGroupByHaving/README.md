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
-- Write a SQL query to find the number of employees whose age is greater than 32.

```sql
-- select count(age) AS COUNT
from employee
where age>32;
```

**Output:**

<img width="307" height="276" alt="image" src="https://github.com/user-attachments/assets/fd91703a-9ae7-4c00-88c0-813f41d80ab5" />


**Question 2**
---
-- Write a SQL query to find the customer with longest name?

```sql
-- select name , max(LENGTH(name)) as length
from customer
```

**Output:**

<img width="596" height="272" alt="image" src="https://github.com/user-attachments/assets/2e731306-2b37-48e6-990d-1293d7ca6077" />


**Question 3**
---
-- Write a SQL query to find the difference between the maximum and minimum price of fruits?

```sql
-- select max(price)-min(price) as price_diff
from fruits
```

**Output:**

<img width="301" height="270" alt="image" src="https://github.com/user-attachments/assets/e17fd7c8-4e0f-425e-8f57-ccde85ecb109" />

**Question 4**
---
-- What is the total number of appointments scheduled for each day?

```sql
-- SELECT DATE(AppointmentDateTime) AS AppointmentDate  , COUNT(*) AS TotalAppointments
FROM Appointments 
GROUP BY AppointmentDateTime;
```

**Output:**

<img width="702" height="588" alt="image" src="https://github.com/user-attachments/assets/4eaed043-5834-4998-a2e4-32d0f9df8bf8" />


**Question 5**
---
-- How many prescriptions were written for each medication?

```sql
-- select Medication ,count(Medication) as TotalPrescriptions
from Prescriptions 
group by Medication;
```

**Output:**

<img width="683" height="674" alt="image" src="https://github.com/user-attachments/assets/2a7cca6d-d541-449e-93ec-40862afe5ce1" />

**Question 6**
---
-- Write SQL query to extract the email domain from each patient's email address and count the number of patients with the same email domain.

```sql
-- SELECT SUBSTR(Email, INSTR(Email, '@')+1) as EmailDomain  , count(*) as TotalPatients
from Patients 
group by EmailDomain;
```

**Output:**

<img width="562" height="311" alt="image" src="https://github.com/user-attachments/assets/36132cfe-6f01-4cb2-aa97-27867de96291" />


**Question 7**
---
-- Write a SQL query to identify the cities (addresses) where the average salary is greater than Rs. 5000, as per the "customer1" table.

```sql
-- select address , AVG(salary)
from customer1
group by address
having AVG(salary)>5000;
```

**Output:**

<img width="513" height="380" alt="image" src="https://github.com/user-attachments/assets/6966b711-217d-4bcd-8066-f34e2ffe148b" />


**Question 8**
---
-- Write the SQL query that accomplishes the selection of average price for each category from the "products" table and includes only those products where the average price falls between 10 and 15.

```sql
-- select category_id  , AVG(Price) 
from products
group by category_id
having AVG(Price) between 10 and 15;
```

**Output:**

<img width="537" height="300" alt="image" src="https://github.com/user-attachments/assets/c53d4622-2f22-42b2-b141-866a2cbe8f89" />


**Question 9**
---
-- Write the SQL query that accomplishes the selection of total cost of all products in each category from the "products" table and includes only those products where the total cost is greater than 50.

```sql
-- select category_id  , sum(price) as Total_Cost
from products
group by category_id
having sum(price)>50;
```

**Output:**

<img width="507" height="297" alt="image" src="https://github.com/user-attachments/assets/95b2da74-43f1-4967-988d-387653fc2fd5" />


**Question 10**
---
-- Write the SQL query that accomplishes the grouping of data by age, calculates the average income for each age group, and includes only those age groups where the average income falls between 300,000 and 500,000.

```sql
-- select age , AVG(income)
from employee
group by age
having AVG(income) between 300000 and 500000;
```

**Output:**

<img width="514" height="291" alt="image" src="https://github.com/user-attachments/assets/cdb21baa-a10b-4418-a936-20db3ea8a00a" />

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/6b6b5e56-a2f9-4a96-9bd8-584a12d3e3cd" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
