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
![image](https://github.com/user-attachments/assets/ae1dcbfe-73ee-4ff7-8cfd-b8eafb82b25e)


```sql
ALTER  TABLE employee 
RENAME COLUMN id TO employee_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/ae106520-faa4-4e95-9e35-c82414ef9830)


**Question 2**
---
![image](https://github.com/user-attachments/assets/50e0f82d-5d35-42f6-bbdd-69d55dc661de)


```sql
CREATE TABLE orders (ord_id TEXT CHECK(LENGTH(ord_id)=4) NOT NULL,
item_id TEXT NOT NULL, ord_date DATE, ord_qty INTEGER, cost INTEGER,
PRIMARY KEY (item_id , ord_date))
```

**Output:**

![image](https://github.com/user-attachments/assets/68707e2a-0122-4b8c-8f1a-88e6774ee7dc)


**Question 3**
---
![image](https://github.com/user-attachments/assets/7e31d9df-a099-4b5f-b040-5f461b4a16e4)


```sql
CREATE TABLE Orders (OrderID INTEGER PRIMARY KEY,
OrderDate DATE NOT NULL,CustomerID INTEGER,
FOREIGN KEY (CustomerID)  REFERENCES Customers(CustomerID));
```

**Output:**

![image](https://github.com/user-attachments/assets/af042f16-6c04-4663-bd56-98f0aca1869e)


**Question 4**
---
![image](https://github.com/user-attachments/assets/5612d666-80c9-494b-b4fc-8b8e660b9bc2)


```sql
INSERT INTO Products ( Name, Category, Price, Stock)
VALUES ( 'Smartphone', 'Electronics', 800, 150),
 ('Headphones','Accessories',200,300);
```

**Output:**

![image](https://github.com/user-attachments/assets/e912d571-97b4-4831-928f-fb2a0341fda0)


**Question 5**
---
![image](https://github.com/user-attachments/assets/e8fddf2f-51e4-47e8-90ff-84b9131182d6)



```sql
CREATE TABLE Products (ProductID INTEGER PRIMARY KEY, ProductName TEXT UNIQUE NOT NULL,
Price REAL CHECK(Price > 0), StockQuantity INTEGER check (StockQuantity >= 0));
```

**Output:**

![image](https://github.com/user-attachments/assets/c180ab29-bbd6-495d-884b-58328c93653c)


**Question 6**
---
![image](https://github.com/user-attachments/assets/77591bd0-fe38-49b8-93cd-4fba0e795e71)


```sql
ALTER TABLE Companies 
RENAME COLUMN name TO first_name;
ALTER TABLE Companies
ADD  mobilenumb number; 
ALTER TABLE Companies
ADD DOB Date;
ALTER TABLE Companies
ADD State varchar(30);
```

**Output:**

![image](https://github.com/user-attachments/assets/e2f0f2d0-608b-4c66-8fbe-69662a566c22)


**Question 7**
---
![image](https://github.com/user-attachments/assets/28fd154c-3619-4275-99a2-a25ef438a476)


```sql
INSERT INTO Customers (CustomerID,Name, Address, Email )
SELECT CustomerID,Name, Address, Email FROM Old_customers;
```

**Output:**

![image](https://github.com/user-attachments/assets/b97e2053-5136-4538-8542-cba425440422)


**Question 8**
---
![image](https://github.com/user-attachments/assets/e0da1365-dcec-4157-9cf9-9c25bce2d842)


```sql
CREATE TABLE Reviews (ReviewID INTEGER, ProductID INTEGER , Rating REAL, ReviewText TEXT);
```

**Output:**

![image](https://github.com/user-attachments/assets/cdee7523-0e7d-439c-9b15-4bf02cfaf70b)


**Question 9**
---
![image](https://github.com/user-attachments/assets/670fc782-7ef8-4a65-83e0-ad04be04a8cd)


```sql
CREATE TABLE Shipments(ShipmentID INTEGER PRIMARY KEY, ShipmentDate DATE ,
SupplierID INTEGER , OrderID  INTEGER,  FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
FOREIGN KEY (OrderID) REFERENCES Orders(OrderID));
```

**Output:**

![image](https://github.com/user-attachments/assets/350e0b2f-7259-4702-8600-b97a41ba88d2)


**Question 10**
---
![image](https://github.com/user-attachments/assets/0f76305d-30e0-4f11-97cb-f6cd51330de6)


```sql
INSERT INTO Employee (EmployeeID,Name,Position)
VALUES (4,'Emily White','Analyst');
```

**Output:**

![image](https://github.com/user-attachments/assets/a5c25156-68e7-4bda-ab00-304a7fb1f903)



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
