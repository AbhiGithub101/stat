---
description: >-
  Answers for the practice questions on database creation, tables, SELECT,
  INSERT, primary keys, and IDENTITY
---

# Practice Questions Answers

## Practice Questions Answers

Use these answers to verify your queries after attempting the practice set.

### Syntax practice answers

#### 1. Create a database named `school_db`

```sql
CREATE DATABASE school_db;
```

#### 2. Switch to `school_db`

```sql
USE school_db;
```

#### 3. Create the `Students` table

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    FullName VARCHAR(100),
    Course VARCHAR(50),
    JoinDate DATE
);
```

#### 4. Display all columns from `Employee`

```sql
SELECT * FROM Employee;
```

#### 5. Display only `FullName` and `Department`

```sql
SELECT FullName, Department FROM Employee;
```

#### 6. Insert one row into `Employee`

```sql
INSERT INTO Employee (ID, FullName, Department, DateOfJoining, Gender, EmailID)
VALUES (109, 'Ankit Sharma', 'IT', '2024-03-12', 'M', 'ankit.sharma@company.com');
```

#### 7. Insert three rows in one query

```sql
INSERT INTO Employee
VALUES
(110, 'Pooja Mehta', 'HR', '2023-07-10', 'F', 'pooja.mehta@company.com'),
(111, 'Rohan Das', 'Finance', '2022-11-25', 'M', 'rohan.das@company.com'),
(112, 'Simran Kaur', 'Sales', '2024-01-05', 'F', 'simran.kaur@company.com');
```

#### 8. Create the `Departments` table

```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(50)
);
```

#### 9. Create `Employee_Auto` with `IDENTITY(1,1)`

```sql
CREATE TABLE Employee_Auto (
    ID INT IDENTITY(1,1) PRIMARY KEY,
    FullName VARCHAR(100),
    Department VARCHAR(50),
    DateOfJoining DATE,
    Gender CHAR(1),
    EmailID VARCHAR(150)
);
```

#### 10. Insert two rows into `Employee_Auto`

```sql
INSERT INTO Employee_Auto (FullName, Department, DateOfJoining, Gender, EmailID)
VALUES ('Nikita Roy', 'IT', '2024-02-01', 'F', 'nikita.roy@company.com');

INSERT INTO Employee_Auto (FullName, Department, DateOfJoining, Gender, EmailID)
VALUES ('Arjun Nair', 'Sales', '2024-02-15', 'M', 'arjun.nair@company.com');
```

### Scenario-based answers

#### 1. New company setup

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

#### 2. Duplicate ID issue

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

#### 3. Data entry without mistakes

```sql
CREATE TABLE Employee (
    ID INT IDENTITY(1001,1) PRIMARY KEY,
    FullName VARCHAR(100),
    Department VARCHAR(50),
    DateOfJoining DATE,
    Gender CHAR(1),
    EmailID VARCHAR(150)
);
```

#### 4. Quick verification after insert

```sql
SELECT FullName, Department FROM Employee;
```

#### 5. Wrong insert order

**1. What is wrong in this query?**

The values are not in the correct column order.

**2. Which rule did they break?**

When all columns are used without naming them, values must match the table column order exactly.

**3. Correct query:**

```sql
INSERT INTO Employee
VALUES (101, 'Rahul Sharma', 'IT', '2022-06-01', 'M', 'rahul@email.com');
```

#### 6. College admissions system

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    FullName VARCHAR(120),
    Course VARCHAR(60),
    AdmissionDate DATE
);
```

### Challenge answers

#### 1. Create a `Books` table

```sql
CREATE TABLE Books (
    BookID INT PRIMARY KEY,
    BookName VARCHAR(100),
    AuthorName VARCHAR(100),
    Price DECIMAL(10,2)
);
```

#### 2. Insert four books in one query

```sql
INSERT INTO Books
VALUES
(1, 'Python Basics', 'Amit Rao', 499.00),
(2, 'SQL Essentials', 'Neha Jain', 599.00),
(3, 'Pandas for Analysis', 'Rohit Mehta', 699.00),
(4, 'Data Visualization', 'Sneha Kapoor', 799.00);
```

#### 3. Show only `BookName` and `Price`

```sql
SELECT BookName, Price FROM Books;
```

#### 4. Create `Books` with `IDENTITY(500,5)`

```sql
CREATE TABLE Books_Auto (
    BookID INT IDENTITY(500,5) PRIMARY KEY,
    BookName VARCHAR(100),
    AuthorName VARCHAR(100),
    Price DECIMAL(10,2)
);
```

{% hint style="success" %}
If your answers match the logic and syntax here, you are ready for the next SQL lesson.
{% endhint %}
