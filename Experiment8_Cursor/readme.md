# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:

- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Steps:**

- Create an `employees` table with fields `emp_id`, `emp_name`, and `designation`.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

**PROGRAM**
```
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50)
);

INSERT INTO employees VALUES (101, 'Arun', 'Manager');
INSERT INTO employees VALUES (102, 'Priya', 'Developer');
INSERT INTO employees VALUES (103, 'Karthik', 'Analyst');

COMMIT;

DECLARE
    CURSOR emp_cursor IS
        SELECT emp_name, designation FROM employees;

    v_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_name, v_designation;
        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE('Employee Name: ' || v_name ||
                             ' | Designation: ' || v_designation);
    END LOOP;

    IF emp_cursor%ROWCOUNT = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

    CLOSE emp_cursor;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```

**Output:**  
The program should display the employee details or an error message.

<img width="502" height="191" alt="image" src="https://github.com/user-attachments/assets/6a8e8291-6e9f-413a-8014-d44bd1d7cc16" />


---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- Modify the `employees` table by adding a `salary` column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.


**PROGRAM**
```
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50)
);


INSERT INTO employees VALUES (101, 'Arun', 'Manager');
INSERT INTO employees VALUES (102, 'Priya', 'Developer');
INSERT INTO employees VALUES (103, 'Karthik', 'Analyst');

COMMIT;


ALTER TABLE employees
ADD salary NUMBER;

UPDATE employees SET salary = 60000 WHERE emp_id = 101;
UPDATE employees SET salary = 45000 WHERE emp_id = 102;
UPDATE employees SET salary = 30000 WHERE emp_id = 103;

COMMIT;

DECLARE
   
    CURSOR emp_cursor(p_min_salary NUMBER, p_max_salary NUMBER) IS
        SELECT emp_name, designation, salary
        FROM employees
        WHERE salary BETWEEN p_min_salary AND p_max_salary;

    v_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;
    v_salary employees.salary%TYPE;

BEGIN
    OPEN emp_cursor(30000, 60000);  

    LOOP
        FETCH emp_cursor INTO v_name, v_designation, v_salary;
        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE('Employee Name: ' || v_name ||
                             ' | Designation: ' || v_designation ||
                             ' | Salary: ' || v_salary);
    END LOOP;

    IF emp_cursor%ROWCOUNT = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

    CLOSE emp_cursor;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found within the given salary range.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
**Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.

<img width="651" height="281" alt="image" src="https://github.com/user-attachments/assets/0470c8b3-4efd-4a0e-ac81-6a63edc378c3" />


---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- Modify the `employees` table by adding a `dept_no` column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.


**PROGRAM**
```
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50)
);


INSERT INTO employees VALUES (101, 'Arun', 'Manager');
INSERT INTO employees VALUES (102, 'Priya', 'Developer');
INSERT INTO employees VALUES (103, 'Karthik', 'Analyst');

COMMIT;


ALTER TABLE employees
ADD dept_no NUMBER;

UPDATE employees SET dept_no = 10 WHERE emp_id = 101;
UPDATE employees SET dept_no = 20 WHERE emp_id = 102;
UPDATE employees SET dept_no = 30 WHERE emp_id = 103;

COMMIT;

DECLARE
    v_count NUMBER;

BEGIN
    
    SELECT COUNT(*) INTO v_count FROM employees;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

    
    FOR emp_rec IN (SELECT emp_name, dept_no FROM employees)
    LOOP
        DBMS_OUTPUT.PUT_LINE('Employee Name: ' || emp_rec.emp_name ||
                             ' | Department No: ' || emp_rec.dept_no);
    END LOOP;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found in the database.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```


**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.

<img width="425" height="192" alt="image" src="https://github.com/user-attachments/assets/c7ae5fc5-c873-40fd-b80d-ba046c19ea1c" />


---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- Modify the `employees` table by adding `emp_id`, `emp_name`, `designation`, and `salary` fields.
- Insert sample data into the `employees` table.
- Declare a cursor using `%ROWTYPE` to fetch complete rows from the `employees` table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

**PROGRAM**
```
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    salary NUMBER
);

INSERT INTO employees VALUES (101, 'Arun', 'Manager', 60000);
INSERT INTO employees VALUES (102, 'Priya', 'Developer', 45000);
INSERT INTO employees VALUES (103, 'Karthik', 'Analyst', 30000);

COMMIT;

DECLARE
    
    CURSOR emp_cursor IS
        SELECT * FROM employees;

   
    emp_rec employees%ROWTYPE;

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO emp_rec;
        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE('Employee ID: ' || emp_rec.emp_id ||
                             ' | Name: ' || emp_rec.emp_name ||
                             ' | Designation: ' || emp_rec.designation ||
                             ' | Salary: ' || emp_rec.salary);
    END LOOP;

    IF emp_cursor%ROWCOUNT = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

    CLOSE emp_cursor;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found in the database.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```

**Output:**  
The program should display employee records or the appropriate error message if no data is found.

<img width="753" height="186" alt="image" src="https://github.com/user-attachments/assets/85f28367-77df-450c-b8ca-ee6d70b48afc" />


---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- Modify the `employees` table to include a `dept_no` and `salary` field.
- Insert sample data into the `employees` table with different department numbers.
- Use a cursor with the `FOR UPDATE` clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle `NO_DATA_FOUND` or other errors that may occur.

**PROGRAM**
```
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    dept_no NUMBER,
    salary NUMBER
);

INSERT INTO employees VALUES (101, 'Arun', 'Manager', 10, 60000);
INSERT INTO employees VALUES (102, 'Priya', 'Developer', 20, 45000);
INSERT INTO employees VALUES (103, 'Karthik', 'Analyst', 10, 30000);
INSERT INTO employees VALUES (104, 'Divya', 'Tester', 30, 35000);

COMMIT;


DECLARE
    CURSOR emp_cursor IS
        SELECT emp_id, emp_name, salary
        FROM employees
        WHERE dept_no = 10
        FOR UPDATE;

    v_count NUMBER := 0;

BEGIN
    FOR emp_rec IN emp_cursor LOOP

        UPDATE employees
        SET salary = salary + 5000
        WHERE CURRENT OF emp_cursor;

        DBMS_OUTPUT.PUT_LINE('Salary updated for: ' || emp_rec.emp_name);

        v_count := v_count + 1;
    END LOOP;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

    COMMIT;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the specified department.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```

**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.

<img width="332" height="171" alt="image" src="https://github.com/user-attachments/assets/c1ec7e29-19fa-4d41-a9ff-3eb1171b10b0" />

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

