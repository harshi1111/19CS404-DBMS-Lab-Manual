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
![image](https://github.com/user-attachments/assets/e5e376bf-9c4a-42d0-b687-41e4c26b4f19)


```sql
UPDATE sales
SET total_sell_price = quantity * sell_price
WHERE product_id = 10;
```

**Output:**

![image](https://github.com/user-attachments/assets/ff64b5db-7535-4c0b-a286-3620be9c858c)


**Question 2**
---
![image](https://github.com/user-attachments/assets/d3a4e486-91b6-4421-807b-c233a926b848)


```sql
UPDATE suppliers
SET supplier_name = 'A1 Suppliers'
WHERE supplier_id = 8;
```

**Output:**

![image](https://github.com/user-attachments/assets/dea1fdde-581a-4eb1-8654-843ee872dc9c)


**Question 3**
---
![image](https://github.com/user-attachments/assets/223b0480-a394-4b21-b1ac-1a4eda944f2a)


```sql
UPDATE products
SET category = 'Household'
WHERE product_name LIKE '%Detergent%'  ;
```

**Output:**

![image](https://github.com/user-attachments/assets/8a3ba06f-ee65-4f20-9d6c-d52717b2ca15)


**Question 4**
![image](https://github.com/user-attachments/assets/3f00c471-2d9b-468e-a4af-d43fd1bca871)


```sql
UPDATE suppliers
SET supplier_name = UPPER(supplier_name)
WHERE contact_person LIKE '%Singh%';
```

**Output:**

![image](https://github.com/user-attachments/assets/a9615dc9-6e58-4c94-8c0f-8dbccb94c284)


**Question 5**
---
![image](https://github.com/user-attachments/assets/609c4acc-af4f-4296-82a5-f64b0dc50cf5)


```sql
UPDATE products 
SET reorder_lvl = 20
WHERE quantity < 10 and category = 'Snacks';
```

**Output:**

![image](https://github.com/user-attachments/assets/2fbaccfa-9073-432f-a571-b31ee0cd3c8f)

**Question 6**
---
![image](https://github.com/user-attachments/assets/4b186a47-d0a8-4c95-8560-2a701f2364a2)


```sql
DELETE FROM doctors 
WHERE specialization IN ('Pediatrics' , 'Cardiology')
AND last_name = 'Brown';
```

**Output:**

![image](https://github.com/user-attachments/assets/e32902eb-45d3-45f3-ab71-23b82fcca339)


**Question 7**
---
![image](https://github.com/user-attachments/assets/35c7b0dd-bbf8-467f-a713-184a3ac84e70)


```sql
DELETE FROM customer
WHERE CUST_NAME LIKE '%Holmes%';
```

**Output:**

![image](https://github.com/user-attachments/assets/ea7f0776-46de-4b7d-b46e-014b81057457)


**Question 8**
---
![image](https://github.com/user-attachments/assets/c8b2736e-9c92-40f1-81da-aef5967f9008)


```sql
DELETE FROM customer
WHERE GRADE < 2;
```

**Output:**

![image](https://github.com/user-attachments/assets/7b4e747c-8ede-4086-a006-151cc54408f7)


**Question 9**
---
![image](https://github.com/user-attachments/assets/3d0c9809-5c10-497e-bdf0-c88a0ddc2d1a)


```sql
DELETE  FROM doctors
WHERE last_name IS NULL;
```

**Output:**

![image](https://github.com/user-attachments/assets/3c144825-dc82-4482-86e1-7b548357ed93)


**Question 10**
---
![image](https://github.com/user-attachments/assets/fdb064d6-cc41-49de-8adc-26e2a5623ce9)


```sql
DELETE FROM customer
WHERE (GRADE = 3 OR AGENT_CODE = 'A008') 
AND OUTSTANDING_AMT < 5000;
```

**Output:**

![image](https://github.com/user-attachments/assets/89d04cd4-6180-44e1-8766-fe6a31759627)


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
