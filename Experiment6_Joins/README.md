# Experiment 6: Joins
# REG_NO : 212224040232

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
Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.



```sql
SELECT 
    c.cust_name AS "cust_name",
    c.city AS "city",
    o.ord_no AS "ord_no",
    o.ord_date AS "ord_date",
    o.purch_amt AS "Order Amount"
FROM 
    customer c
LEFT JOIN 
    orders o 
ON 
    c.customer_id = o.customer_id
ORDER BY 
    o.ord_date ASC;
```

**Output:**

<img width="1279" height="956" alt="image" src="https://github.com/user-attachments/assets/a83a42ad-14b7-4de3-8629-b160fef3134c" />


**Question 2**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  



```sql
SELECT 
    c.cust_name AS "Customer Name",
    c.city AS "city",
    s.name AS "Salesman",
    s.city AS "city",
    s.commission AS "commission"
FROM 
    customer c
JOIN 
    salesman s
ON 
    c.salesman_id = s.salesman_id
WHERE 
    c.city <> s.city
    AND s.commission > 0.12;

```

**Output:**

<img width="1289" height="488" alt="image" src="https://github.com/user-attachments/assets/cf7fb4f0-e4ec-4797-9fca-d2b1a25065c9" />


**Question 3**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

```sql
SELECT
    s.name AS Salesman,
    c.cust_name,
    s.city
FROM
    salesman s
JOIN
    customer c ON s.city = c.city;
```

**Output:**

<img width="1049" height="664" alt="image" src="https://github.com/user-attachments/assets/b2379be9-07b7-435a-a176-9fd23354f8e2" />


**Question 4**
---
 From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

```sql
SELECT 
    c.cust_name AS "Customer Name",
    c.city AS "city",
    s.name AS "Salesman",
    s.commission AS "commission"
FROM 
    customer c
JOIN 
    salesman s
ON 
    c.salesman_id = s.salesman_id
WHERE 
    s.commission > 0.12;

```

**Output:**

<img width="1119" height="604" alt="image" src="https://github.com/user-attachments/assets/ceaadc17-6a09-4e08-b5e6-3935c0170acd" />


**Question 5**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

<img width="1052" height="172" alt="image" src="https://github.com/user-attachments/assets/85d3fb9b-2aa2-4a3b-a338-5b2f246e2653" />
APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date
<img width="1039" height="169" alt="image" src="https://github.com/user-attachments/assets/ef26ccdc-3a77-4af1-8844-6449b2786db7" />


```sql
SELECT 
    p.first_name AS patient_name,
    a.appointment_id,
    a.patient_id,
    a.doctor_id,
    a.appointment_date
FROM 
    patients p
INNER JOIN 
    appointments a
ON 
    p.patient_id = a.patient_id;

```

**Output:**

<img width="1285" height="497" alt="image" src="https://github.com/user-attachments/assets/5068156f-994e-444c-8077-f4e377a99846" />


**Question 6**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the test name from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
<img width="1052" height="172" alt="image" src="https://github.com/user-attachments/assets/b44ac449-f49f-42d6-a2b2-3dc95050441e" />
TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date
<img width="1060" height="171" alt="image" src="https://github.com/user-attachments/assets/fe6b45bf-4072-42e8-86e1-8eca0d64792d" />


```sql
SELECT 
    p.first_name AS patient_name,
    t.test_name
FROM 
    patients p
INNER JOIN 
    test_results t
ON 
    p.patient_id = t.patient_id;

```

**Output:**

<img width="776" height="535" alt="image" src="https://github.com/user-attachments/assets/ce1865c2-003b-4095-99ad-a130d78d62cc" />


**Question 7**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman with the name 'Mc Lyon'.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

```sql
SELECT 
    c.*
FROM 
    customer c
LEFT JOIN 
    salesman s
ON 
    c.salesman_id = s.salesman_id
WHERE 
    s.name = 'Mc Lyon';

```

**Output:**

<img width="1269" height="372" alt="image" src="https://github.com/user-attachments/assets/67770dda-77a8-4d2b-bfc0-24dc3d8ebf2c" />


**Question 8**
---
Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column. Include conditions to filter for patients discharged between '2024-03-01' and '2024-03-31' but not admitted during the same period.


```sql
SELECT 
    p.first_name,
    s.*
FROM 
    patients p
INNER JOIN 
    surgeries s
ON 
    p.patient_id = s.patient_id
WHERE 
    p.discharge_date BETWEEN '2024-03-01' AND '2024-03-31'
    AND (
        p.admission_date < '2024-03-01'
        OR p.admission_date > '2024-03-31'
    );

```

**Output:**

<img width="1265" height="371" alt="image" src="https://github.com/user-attachments/assets/f4911bc7-3d78-45d6-9b0c-ceb4a69940ee" />

**Question 9**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

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

<img width="1235" height="469" alt="image" src="https://github.com/user-attachments/assets/b09ba9b3-5c4b-4abe-86c9-72c336b72501" />

**Question 10**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.


```sql
SELECT 
    o.ord_no,
    o.purch_amt,
    c.cust_name,
    c.city
FROM 
    orders o
INNER JOIN 
    customer c
ON 
    o.customer_id = c.customer_id
WHERE 
    o.purch_amt BETWEEN 500 AND 2000;

```

**Output:**

<img width="1259" height="403" alt="image" src="https://github.com/user-attachments/assets/d9573713-85c2-47e7-847b-879fca064bfe" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
