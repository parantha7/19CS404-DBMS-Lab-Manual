# Experiment 4: Aggregate Functions, Group By and Having Clause
# REG_NO : 212224040232

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
What is the average dosage prescribed for each medication?

Sample tablePrescriptions Table
<img width="1082" height="154" alt="image" src="https://github.com/user-attachments/assets/dbe2aa2a-80d6-4c06-b3e7-06e8721ad590" />


```sql
select Medication,avg(Dosage) as AvgDosage from Prescriptions group by Medication;
```

**Output:**

<img width="506" height="667" alt="image" src="https://github.com/user-attachments/assets/d12cd9e6-58c5-4d31-a795-75fb08b16d79" />


**Question 2**
---
How many doctors specialize in each medical specialty?

Sample table:Doctors Table
<img width="1039" height="162" alt="image" src="https://github.com/user-attachments/assets/c96aaf11-98cb-4cd7-9cb9-92aeffd49605" />

```sql
select Specialty,count(*) as TotalDocto from Doctors group by Specialty
```

**Output:**

<img width="614" height="605" alt="image" src="https://github.com/user-attachments/assets/88693c0c-9265-4000-b6ee-8adddecc54ea" />


**Question 3**
---
What is the count of male and female patients?

Sample table: Patients Table

<img width="1076" height="161" alt="image" src="https://github.com/user-attachments/assets/89dee758-eed2-4cf2-9a2e-d16233d44a02" />

```sql
select gender,count(*) as TotalPatients from Patients group by gender
```

**Output:**

<img width="505" height="340" alt="image" src="https://github.com/user-attachments/assets/049b98e7-100a-4b8a-9abb-fb4a0d2fcd5f" />


**Question 4**
---
Write a SQL query to find the total number of unique cities in the customer table?
```
Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
```

```sql
select count(distinct city) as unique_cities from customer 
```

**Output:**

<img width="416" height="297" alt="image" src="https://github.com/user-attachments/assets/502ee5a8-9e96-4629-914d-93ba4b4e5bc9" />


**Question 5**
---
Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai city
```
Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
```
```sql
select avg(length(email)) as avg_email_length_below_30 from customer where city='Mumbai'
```

**Output:**

<img width="484" height="306" alt="image" src="https://github.com/user-attachments/assets/8568d231-0ea1-4bc4-b13b-1538d52eec97" />


**Question 6**
---
Write a SQL query to find the minimum purchase amount.
  ```
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001
```
```sql
select min(purch_amt) as MINIMUM from orders
```

**Output:**

<img width="308" height="306" alt="image" src="https://github.com/user-attachments/assets/990a90d6-9e1b-425e-b031-e7785f603cb2" />


**Question 7**
---
Write a SQL query to return the total number of rows in the 'customer' table where the city is not Noida.

Sample table: customer

<img width="668" height="138" alt="image" src="https://github.com/user-attachments/assets/2049ffbc-2620-40a8-8989-fdbc897c1bcb" />

```sql
select count(*) as `COUNT` from customer where city <> 'Noida'
```

**Output:**

<img width="330" height="309" alt="image" src="https://github.com/user-attachments/assets/3e160139-8781-498e-a895-5c89a5fce3b1" />


**Question 8**
---
Write the SQL query that accomplishes the grouping of data by age intervals using the expression (age/5)5, calculates the minimum age for each group, and excludes groups where the minimum age is not less than 25.

Sample table: customer1

<img width="992" height="173" alt="image" src="https://github.com/user-attachments/assets/6fe4969a-faa0-42ba-b56b-6be89a747291" />

```sql
select (age/5)*5 as age_group, min(age) as `MIN(age)` from customer1 group by (age/5)*5 having MIN(age) < 25;
```

**Output:**

<img width="463" height="316" alt="image" src="https://github.com/user-attachments/assets/7e369a46-4643-412c-a04d-021210008e82" />


**Question 9**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the average work hours for each date, and excludes dates where the average work hour is not less than 10.

Sample table: employee1

<img width="1031" height="203" alt="image" src="https://github.com/user-attachments/assets/7aafe6ce-08d2-4839-af5c-e07a18ad7516" />

```sql
select jdate,avg(workhour) as `AVG(workhour)` from employee1 group by jdate having avg(workhour) < 10
```

**Output:**

<img width="524" height="329" alt="image" src="https://github.com/user-attachments/assets/a3f586ea-d093-4e1a-9e3a-2846a2812fcb" />


**Question 10**
---
Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.

Sample table: employee

<img width="1011" height="215" alt="image" src="https://github.com/user-attachments/assets/139774c9-9427-4f37-ad5e-c72b26d71d65" />


```sql
select city,sum(Income) as Income from employee group by city having Income >200000
```

**Output:**

<img width="444" height="476" alt="image" src="https://github.com/user-attachments/assets/99dc5c7e-f8e6-4bbc-a15d-ab084bd5610d" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
