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
![image](https://github.com/user-attachments/assets/aa0ef303-3692-4152-aadb-b21fee2d74a5)


```sql
SELECT 
    p.first_name AS patient_name, 
    d.first_name AS doctor_name
FROM 
    patients p
INNER JOIN 
    doctors d ON p.doctor_id = d.doctor_id
WHERE 
    p.date_of_birth > '1990-01-01';

```

**Output:**

![image](https://github.com/user-attachments/assets/e9b13b45-7281-4e63-a1d6-4e860bd7c025)


**Question 2**
---
![image](https://github.com/user-attachments/assets/3be4db12-8f71-4bec-bd23-21cd149fb0c7)


```sql
SELECT 
    c.cust_name, 
    o.ord_no, 
    o.ord_date, 
    o.purch_amt
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id;

```

**Output:**

![image](https://github.com/user-attachments/assets/b7a405ea-6f48-4b60-b4c5-c0e57318bf45)


**Question 3**
---
![image](https://github.com/user-attachments/assets/1c8ea6e3-cb70-4800-9a1c-ebdadadd33aa)


```sql
SELECT 
    o.ord_no, 
    o.purch_amt, 
    c.cust_name, 
    c.city
FROM 
    orders o
JOIN 
    customer c ON o.customer_id = c.customer_id
WHERE 
    o.purch_amt BETWEEN 500 AND 2000;

```

**Output:**

![image](https://github.com/user-attachments/assets/2ef3d3b0-ba52-49c6-9302-91ec3b7d5993)


**Question 4**
---
![image](https://github.com/user-attachments/assets/086d5369-4964-46e3-8426-38ac8e3ca6bf)


```sql
SELECT 
    c.cust_name, 
    c.city, 
    o.ord_no, 
    o.ord_date, 
    o.purch_amt AS "Order Amount"
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
ORDER BY 
    o.ord_date ASC
```

**Output:**

![image](https://github.com/user-attachments/assets/93e5418c-5697-458c-89b7-d2c5ab3fff83)


**Question 5**
---
![image](https://github.com/user-attachments/assets/ab319dcc-a16a-467a-912d-d6bbbd0ce183)


```sql
SELECT 
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    c.cust_name,
    c.city AS customer_city,
    c.grade,
    s.name AS salesman_name,
    s.city AS salesman_city,
    s.commission
FROM 
    orders o
JOIN 
    customer c ON o.customer_id = c.customer_id
JOIN 
    salesman s ON o.salesman_id = s.salesman_id;

```

**Output:**

![image](https://github.com/user-attachments/assets/9a642ab1-339f-4263-8cdb-aec53c3e83df)


**Question 6**
---
![image](https://github.com/user-attachments/assets/69113971-0901-4081-89a6-43e84aaec753)


```sql
SELECT 
    p.*, 
    d.first_name AS doctor_name
FROM 
    patients p
INNER JOIN 
    doctors d ON p.doctor_id = d.doctor_id;

```

**Output:**

![image](https://github.com/user-attachments/assets/2726b0b4-0677-4e6a-b0d0-7b6552317ea9)


**Question 7**
---
![image](https://github.com/user-attachments/assets/d586ae1a-189f-4a46-8dc3-fda589d30556)


```sql
SELECT 
    customer.cust_name AS "Customer Name", 
    customer.city AS "city", 
    salesman.name AS "Salesman", 
    salesman.commission AS "commission"
FROM 
    customer
INNER JOIN 
    salesman ON customer.salesman_id = salesman.salesman_id;

```

**Output:**

![image](https://github.com/user-attachments/assets/b35f4195-fbd0-44f1-ba4c-e374ebe22b27)


**Question 8**
---
![image](https://github.com/user-attachments/assets/dbd65002-3224-4520-a778-cd220c85b01c)


```sql
SELECT 
    customer.cust_name AS "cust_name", 
    customer.city AS "city", 
    customer.grade AS "grade", 
    salesman.name AS "Salesman", 
    salesman.city AS "city"
FROM 
    customer
INNER JOIN 
    salesman ON customer.salesman_id = salesman.salesman_id
WHERE 
    customer.grade < 300
ORDER BY 
    customer.customer_id ASC;

```

**Output:**

![image](https://github.com/user-attachments/assets/a7738429-65bd-4075-8ba9-be52cc4ed452)


**Question 9**
---
![image](https://github.com/user-attachments/assets/684fc20d-630b-4d05-b923-ca3d25fab3d6)


```sql
SELECT 
    c.cust_name
FROM 
    customer AS c
LEFT JOIN 
    orders AS o ON c.customer_id = o.customer_id
WHERE 
    o.purch_amt < 100;

```

**Output:**

![image](https://github.com/user-attachments/assets/6ac2b3c5-cdbc-4763-8841-f6e70b87026b)


**Question 10**
---
![image](https://github.com/user-attachments/assets/2898f186-b890-4030-bf1b-1d10733cebaa)


```sql
SELECT 
    p.*, 
    d.specialization AS doctor_specialization
FROM 
    patients p
INNER JOIN 
    doctors d ON p.doctor_id = d.doctor_id;


```

**Output:**

![image](https://github.com/user-attachments/assets/f90a182e-cfd5-46ee-8ebf-af07046eb23d)



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
