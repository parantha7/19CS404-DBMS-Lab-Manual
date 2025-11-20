# Experiment 2: DDL Commands
# Reg_No : 212224040232

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
Create a new table named item with the following specifications and constraints:

  item_id as TEXT and as primary key.
  
  item_desc as TEXT.
  
  rate as INTEGER.
  
  icom_id as TEXT with a length of 4.
  
  icom_id is a foreign key referencing com_id in the company table.
  
  The foreign key should cascade updates and deletes.
  
  item_desc and rate should not accept NULL.
  

```sql
CREATE TABLE item(
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id TEXT(4),
FOREIGN KEY(icom_id)
REFERENCES company (com_id)
ON UPDATE CASCADE
ON DELETE CASCADE
);
```

**Output:**

<img width="1255" height="322" alt="image" src="https://github.com/user-attachments/assets/12d0005d-a8ae-445f-bc36-47b2b24e30cd" />


**Question 2**
---
Create a table named Attendance with the following constraints:

  AttendanceID as INTEGER should be the primary key.
  
  EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
  
  AttendanceDate as DATE.
  
  Status as TEXT should be one of 'Present', 'Absent', 'Leave'.
  

```sql
CREATE TABLE Attendance(
AttendanceID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
AttendanceDate DATE, 
Status TEXT CHECK(Status IN('Present','Absent','Leave')),
FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1298" height="303" alt="image" src="https://github.com/user-attachments/assets/0dd953cb-a9e1-4764-be3a-74f5ab247573" />

**Question 3**
---
Write a SQL Query  to add attribute Date_of_joining as Date and rename the attribute job_title as Designation in the table 'Employees'

```sql
ALTER TABLE Employees
ADD COLUMN Date_of_joining Date;

ALTER TABLE Employees
RENAME COLUMN job_title TO Designation;
```

**Output:**

<img width="1294" height="344" alt="image" src="https://github.com/user-attachments/assets/099e071d-c9aa-439a-94f3-5ca8b371c48e" />


**Question 4**
---
Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.
```
RollNo      Name          Gender      
----------  ------------  ----------  
204         Samuel Black  M          
```

Note: The Subject and MARKS columns will use their default values.

```sql
INSERT INTO Student_details(RollNo,Name,Gender)
VALUES(204,'Samuel Black','M');
```

**Output:**

<img width="974" height="322" alt="image" src="https://github.com/user-attachments/assets/79ae86ba-e988-44c4-ab6f-26fc3450c1a1" />


**Question 5**
---
Create a table named ProjectAssignments with the following constraints:
  AssignmentID as INTEGER should be the primary key.
  
  EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
  
  ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
  
  AssignmentDate as DATE should be NOT NULL.

```sql
CREATE TABLE ProjectAssignments(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE NOT NULL,
FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID),
FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**

<img width="1291" height="312" alt="image" src="https://github.com/user-attachments/assets/aa97ce4d-cf0f-4414-9bee-ce1249611f08" />


**Question 6**
---
Create a table named Department with the following constraints:

  DepartmentID as INTEGER should be the primary key.
  
  DepartmentName as TEXT should be unique and not NULL.
  
  Location as TEXT.

```sql
CREATE TABLE Department(
DepartmentID INTEGER,
DepartmentName TEXT UNIQUE NOT NULL,
Location TEXT
);
```

**Output:**

<img width="1290" height="301" alt="image" src="https://github.com/user-attachments/assets/bbf842b2-e6b4-489b-ac3d-6c4d724b7fa0" />

**Question 7**
---
Write a SQL Query for inserting the below values in the table Customers
  ```
ID               NAME             AGE  ADDRESS     SALARY      
---------------  ---------------  ---  ----------  ----------  
1                Ramesh           32   Ahmedabad   2000
2                Khilan           25   Delhi       1500
3                Kaushik          23   Kota        2000
```
```sql
INSERT INTO Customers(ID,NAME,AGE,ADDRESS,SALARY)
VALUES(1,'Ramesh',32,'Ahmedabad',2000);
INSERT INTO Customers(ID,NAME,AGE,ADDRESS,SALARY)
VALUES(2,'Khilan',25,'Delhi',1500);
INSERT INTO Customers(ID,NAME,AGE,ADDRESS,SALARY)
VALUES(3,'Kaushik',23,'Kota',2000);
```

**Output:**

<img width="1181" height="290" alt="image" src="https://github.com/user-attachments/assets/c4b0c540-ac65-4c81-8d53-903c34cea007" />

**Question 8**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished
```sql
INSERT INTO Books(ISBN, Title, Author, Publisher, YearPublished)
SELECT ISBN, Title, Author, Publisher, YearPublished 
FROM Out_of_print_books;
```

**Output:**

<img width="1290" height="296" alt="image" src="https://github.com/user-attachments/assets/2d8446e6-c6c3-40a5-a2c8-719be9f2ca8e" />

**Question 9**
---
Create a table named Orders with the following columns:

  OrderID as INTEGER
  
  OrderDate as TEXT
  
  CustomerID as INTEGER


```sql
CREATE TABLE Orders(
OrderID INTEGER,
OrderDate TEXT,
CustomerID INTEGER
);
```

**Output:**

<img width="1280" height="363" alt="image" src="https://github.com/user-attachments/assets/5463d718-af6a-40d6-98c7-bcc162ff45bf" />

**Question 10**
---
Write a SQL query to Add a new column mobilenumber as number in the Student_details table.

Sample table: Student_details
```
 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
```
```sql
ALTER TABLE Student_details
ADD COLUMN mobilenumb number;
```

**Output:**

<img width="1285" height="369" alt="image" src="https://github.com/user-attachments/assets/7ce00b6d-3654-4005-ad5f-d6641c2d0074" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
