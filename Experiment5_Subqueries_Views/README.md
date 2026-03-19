# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
-- Write a SQL query to List departments with names longer than the average length

```sql
-- select department_id,department_name
from Departments 
WHERE LENGTH(department_name)>(SELECT AVG(LENGTH(department_name)) from Departments);
```

**Output:**

<img width="483" height="342" alt="image" src="https://github.com/user-attachments/assets/7fe9229f-6022-4b8e-a68c-22a24b57cc03" />


**Question 2**
---
-- From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

```sql
-- select ord_no, purch_amt, ord_date, customer_id , salesman_id
from ORDERS 
where salesman_id IN(
select salesman_id 
from SALESMAN 
where city = "New York"
);
```

**Output:**

<img width="1119" height="426" alt="image" src="https://github.com/user-attachments/assets/1fc02ea2-6539-41ee-9f44-dca1a334e35c" />


**Question 3**
---
-- Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million


```sql
-- select *
from Employee 
where age <(Select AVG(age) FROM Employee where income>1000000);
```

**Output:**

<img width="1222" height="356" alt="image" src="https://github.com/user-attachments/assets/069c7ef4-8fcb-4e2b-94a4-45ac1f1dc756" />


**Question 4**
---
-- Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

```sql
-- SELECT name
from customer
where phone IN(
select phone
from customer
group by phone
having count(*)=1
);
```

**Output:**

<img width="379" height="402" alt="image" src="https://github.com/user-attachments/assets/eef1e039-b149-4068-ba8a-b61212e0dd61" />


**Question 5**
---
-- Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

```sql
-- select *
from CUSTOMERS
where SALARY >4500;
```

**Output:**

<img width="1080" height="371" alt="image" src="https://github.com/user-attachments/assets/24c9b1c6-2ed8-4ede-bb59-2b9aed1f3db3" />


**Question 6**
---
-- From the following tables, write a SQL query to determine the commission of the salespeople in Paris. Return commission.

```sql
-- select commission 
from salesman 
where salesman_id  IN(
select salesman_id  
from customer 
where city = 'Paris'
);
```

**Output:**

<img width="307" height="285" alt="image" src="https://github.com/user-attachments/assets/86e0c796-670c-499b-bede-42906a055aa4" />


**Question 7**
---
-- From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

```sql
-- select grade , COUNT(*)
from customer 
where grade >(
select AVG(grade)
from customer 
where city ='New York'
)
group by grade;
```

**Output:**

<img width="485" height="272" alt="image" src="https://github.com/user-attachments/assets/b5cb9075-7781-41a9-badb-8d4c500cbf54" />


**Question 8**
---
-- From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

```sql
-- select  ord_no, purch_amt, ord_date, customer_id , salesman_id
from orders
where salesman_id IN(
 select salesman_id
 from Salesman
 where name ='Paul Adam'
 );
```

**Output:**

<img width="1108" height="327" alt="image" src="https://github.com/user-attachments/assets/faae5b15-7311-4cb0-b187-a85c28bfc920" />


**Question 9**
---
-- Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

```sql
-- select student_name,grade
from GRADES
where (subject, grade)IN(
Select subject ,MAX(grade)
from GRADES
GROUP BY subject
);
```

**Output:**

<img width="657" height="386" alt="image" src="https://github.com/user-attachments/assets/1157dc38-a171-4df1-914e-a542ef135e3c" />


**Question 10**
---
-- Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

```sql
-- SELECT *
FROM customer 
where customer_id  = (
select salesman_id
from salesman 
where name='Mc Lyon'
)-2001;
```

**Output:**

<img width="1120" height="265" alt="image" src="https://github.com/user-attachments/assets/bbe49d23-5859-485b-af07-f20dff66846f" />

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/b954bb3d-ba88-4133-8557-fca8b5cc1a4e" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
