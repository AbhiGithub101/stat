---
description: >-
  Practice questions for database creation, tables, SELECT, INSERT, primary
  keys, and IDENTITY
---

# Database Creation Assignment

## Practice Questions

Use these questions to practice database creation, table creation, `SELECT`, `INSERT`, primary keys.

### Syntax practice

1. Write a query to create a database named `school_db`.

<details>

<summary>Solution</summary>

```sql
CREATE DATABASE school_db;
```

</details>

2. Write a query to switch your session to `school_db`.

<details>

<summary>Solution</summary>

```sql
USE school_db;
```

</details>

3. Create a table named `Students` with these columns:
   * `StudentID` as `INT PRIMARY KEY`
   * `FullName` as `VARCHAR(100)`
   * `Course` as `VARCHAR(50)`
   * `JoinDate` as `DATE`

<details>

<summary>Solution</summary>

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    FullName VARCHAR(100),
    Course VARCHAR(50),
    JoinDate DATE
);
```

</details>

4. Write a query to display all columns from the `Employee` table.

<details>

<summary>Solution</summary>

```sql
SELECT * FROM Employee;
```

</details>

5. Write a query to display only `FullName` and `Department` from the `Employee` table.

<details>

<summary>Solution</summary>

```sql
SELECT FullName, Department FROM Employee;
```

</details>

6. Insert one row into `Employee` with your own sample values.

<details>

<summary>Solution</summary>

```sql
INSERT INTO Employee (ID, FullName, Department, DateOfJoining, Gender, EmailID)
VALUES (109, 'Ankit Sharma', 'IT', '2024-03-12', 'M', 'ankit.sharma@company.com');
```

</details>

7. Insert three rows into `Employee` in a single query.

<details>

<summary>Solution</summary>

```sql
INSERT INTO Employee
VALUES
(110, 'Pooja Mehta', 'HR', '2023-07-10', 'F', 'pooja.mehta@company.com'),
(111, 'Rohan Das', 'Finance', '2022-11-25', 'M', 'rohan.das@company.com'),
(112, 'Simran Kaur', 'Sales', '2024-01-05', 'F', 'simran.kaur@company.com');
```

</details>

8. Create a table named `Departments` with:
   * `DepartmentID` as `INT PRIMARY KEY`
   * `DepartmentName` as `VARCHAR(50)`

<details>

<summary>Solution</summary>

```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(50)
);
```

</details>

### Scenario-based practice

#### 1. New company setup

A startup wants to store employee records in SQL Server.

Write the queries to:

* create a database named `startup_db`
* use that database
* create an `Employee` table with `ID`, `FullName`, `Department`, `DateOfJoining`, `Gender`, and `EmailID`

<details>

<summary>Solution</summary>

```sql
CREATE DATABASE startup_db;
USE startup_db;

CREATE TABLE Employee (
    ID INT PRIMARY KEY,
    FullName VARCHAR(100),
    Department VARCHAR(50),
    DateOfJoining DATE,
    Gender CHAR(1),
    EmailID VARCHAR(150)
);
```

</details>

#### 2. ID issue

A user runs this query:

```sql
INSERT INTO Employee (ID, FullName, Department, DateOfJoining, Gender, EmailID)
VALUES (101, 'Aman Verma', 'IT', '2024-01-10', 'M', 'aman@email.com');
```

But `ID = 101` already exists.

Answer these:

1. What error will happen?
2. Why does it happen?
3. How would you fix the insert?

<details>

<summary>Solution</summary>

**1. What error will happen?**

A primary key violation error will happen.

**2. Why does it happen?**

`ID` is a primary key, so duplicate values are not allowed.

**3. How would you fix the insert?**

Use a new unique ID.

```sql
INSERT INTO Employee (ID, FullName, Department, DateOfJoining, Gender, EmailID)
VALUES (113, 'Aman Verma', 'IT', '2024-01-10', 'M', 'aman@email.com');
```

</details>

#### 3. insert order

A student writes this query:

```sql
INSERT INTO Employee
VALUES ('Rahul Sharma', 101, 'IT', '2022-06-01', 'M', 'rahul@email.com');
```

Answer these:

1. What is wrong in this query?
2. Which rule of `INSERT` did they break?
3. How should the query be corrected?

<details>

<summary>Solution</summary>

**1. What is wrong in this query?**

The values are not in the correct column order.

**2. Which rule did they break?**

When all columns are used without naming them, values must match the table column order exactly.

**3. Correct query:**

```sql
INSERT INTO Employee
VALUES (101, 'Rahul Sharma', 'IT', '2022-06-01', 'M', 'rahul@email.com');
```

</details>

#### 4. College admissions system

A college wants to store student records with these rules:

* each student must have a unique ID
* the full name can store up to 120 characters
* the course name can store up to 60 characters
* the admission date should store only the date

Write the query to create this table.

<details>

<summary>Solution</summary>

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    FullName VARCHAR(120),
    Course VARCHAR(60),
    AdmissionDate DATE
);
```

</details>

### Challenge questions

1. Create a table named `Books` with `BookID`, `BookName`, `AuthorName`, and `Price`.

<details>

<summary>Solution</summary>

```sql
CREATE TABLE Books (
    BookID INT PRIMARY KEY,
    BookName VARCHAR(100),
    AuthorName VARCHAR(100),
    Price DECIMAL(10,2)
);
```

</details>

2. Insert four books in a single query.

<details>

<summary>Solution</summary>

```sql
INSERT INTO Books
VALUES
(1, 'Python Basics', 'Amit Rao', 499.00),
(2, 'SQL Essentials', 'Neha Jain', 599.00),
(3, 'Pandas for Analysis', 'Rohit Mehta', 699.00),
(4, 'Data Visualization', 'Sneha Kapoor', 799.00);
```

</details>

3. Show only `BookName` and `Price` from the table.

<details>

<summary>Solution</summary>

```sql
SELECT BookName, Price FROM Books;
```

</details>
