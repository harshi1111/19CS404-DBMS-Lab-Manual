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

**Output:**  
The program should display the employee details or an error message.

---
**Program:** 
```
-- Step 1: Create the employees table (drop if exists)
DROP TABLE IF EXISTS employees;

CREATE TABLE employees (
    emp_id INT,
    emp_name VARCHAR(50),
    designation VARCHAR(50)
);

-- Step 2: Insert sample data
INSERT INTO employees VALUES 
(101, 'Alice Johnson', 'Developer'),
(102, 'Bob Smith', 'Manager'),
(103, 'Cathy Brown', 'Analyst');

-- Step 3: Stored Procedure with Cursor
DELIMITER $$

CREATE PROCEDURE fetch_employees()
BEGIN
    DECLARE done INT DEFAULT 0;
    DECLARE v_emp_name VARCHAR(50);
    DECLARE v_designation VARCHAR(50);

    -- Declare the cursor
    DECLARE emp_cursor CURSOR FOR 
        SELECT emp_name, designation FROM employees;

    -- Declare continue handler
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;

    -- Open and fetch from the cursor
    OPEN emp_cursor;

    read_loop: LOOP
        FETCH emp_cursor INTO v_emp_name, v_designation;
        IF done THEN
            LEAVE read_loop;
        END IF;
        SELECT CONCAT('Name: ', v_emp_name, ', Designation: ', v_designation) AS employee_info;
    END LOOP;

    CLOSE emp_cursor;
END$$

DELIMITER ;

-- Step 4: Call the procedure
CALL fetch_employees();

```
**Program Output:** 

![image](https://github.com/user-attachments/assets/4afde33e-c81f-4714-bade-c5be2842b095)

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

**Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.

---
**Program:**  
```
-- Step 1: Create the employees table
CREATE TABLE employees (
    emp_id INT PRIMARY KEY AUTO_INCREMENT,
    emp_name VARCHAR(100),
    designation VARCHAR(100),
    salary DECIMAL(10, 2)
);

-- Step 2: Insert sample data into the employees table
INSERT INTO employees (emp_name, designation, salary) 
VALUES
('Alice Johnson', 'Developer', 50000.00),
('Bob Smith', 'Manager', 70000.00),
('Cathy Brown', 'Analyst', 60000.00),
('David Williams', 'Developer', 45000.00),
('Eva Clark', 'Manager', 80000.00);

-- Step 3: Create a stored procedure to use a cursor with parameters
DELIMITER $$

CREATE PROCEDURE GetEmployeesBySalaryRange(IN min_salary DECIMAL(10, 2), IN max_salary DECIMAL(10, 2))
BEGIN
    -- Declare variables for employee details
    DECLARE v_emp_name VARCHAR(100);
    DECLARE v_designation VARCHAR(100);
    DECLARE v_salary DECIMAL(10, 2);
    
    -- Declare the cursor to fetch employees within the salary range
    DECLARE emp_cursor CURSOR FOR
        SELECT emp_name, designation, salary
        FROM employees
        WHERE salary BETWEEN min_salary AND max_salary;

    -- Declare a handler for when no data is found
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET v_emp_name = NULL;

    -- Open the cursor
    OPEN emp_cursor;

    -- Fetch employee details
    FETCH_LOOP: LOOP
        FETCH emp_cursor INTO v_emp_name, v_designation, v_salary;
        
        -- If no more rows are found, exit the loop
        IF v_emp_name IS NULL THEN
            LEAVE FETCH_LOOP;
        END IF;

        -- Display the employee details
        SELECT CONCAT('Employee Name: ', v_emp_name, ', Designation: ', v_designation, ', Salary: ', v_salary) AS employee_info;
    END LOOP;

    -- Close the cursor
    CLOSE emp_cursor;

    -- Check if no rows were fetched
    IF v_emp_name IS NULL THEN
        SELECT 'No employees found in the specified salary range.' AS error_message;
    END IF;
END $$

-- Step 4: Set the delimiter back to default
DELIMITER ;

-- Step 5: Call the stored procedure with a salary range
CALL GetEmployeesBySalaryRange(55000, 75000);

```
**Program Output:**  

![image](https://github.com/user-attachments/assets/a0beb9c8-9ea9-4be0-aa2a-a8c4a5c7158b)

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

**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.

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

**Output:**  
The program should display employee records or the appropriate error message if no data is found.

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

**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

