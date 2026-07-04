---
description: >-
  Practice questions for database creation, tables, SELECT, INSERT, primary
  keys, and IDENTITY
---

# Practice Questions

## Practice Questions

Use these questions to practice database creation, table creation, `SELECT`, `INSERT`, primary keys, and `IDENTITY`.

{% hint style="info" %}
Try to write the queries on your own first. Run them in SQL Server and check the result after each step.
{% endhint %}

### Syntax practice

1. Write a query to create a database named `school_db`.
2. Write a query to switch your session to `school_db`.
3. Create a table named `Students` with these columns:
   * `StudentID` as `INT PRIMARY KEY`
   * `FullName` as `VARCHAR(100)`
   * `Course` as `VARCHAR(50)`
   * `JoinDate` as `DATE`
4. Write a query to display all columns from the `Employee` table.
5. Write a query to display only `FullName` and `Department` from the `Employee` table.
6. Insert one row into `Employee` with your own sample values.
7. Insert three rows into `Employee` in a single query.
8. Create a table named `Departments` with:
   * `DepartmentID` as `INT PRIMARY KEY`
   * `DepartmentName` as `VARCHAR(50)`
9. Create a new `Employee_Auto` table where `ID` is generated automatically using `IDENTITY(1,1)`.
10. Insert two rows into `Employee_Auto` without writing values for the `ID` column.

### Scenario-based practice

#### 1. New company setup

A startup wants to store employee records in SQL Server.

Write the queries to:

* create a database named `startup_db`
* use that database
* create an `Employee` table with `ID`, `FullName`, `Department`, `DateOfJoining`, `Gender`, and `EmailID`

#### 2. Duplicate ID issue

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

#### 3. Data entry without mistakes

An HR team keeps forgetting the last used employee ID.

Write a table creation query that solves this problem by using auto-generated IDs starting from `1001`.

#### 4. Quick verification after insert

You inserted multiple employees into the `Employee` table. Now your manager only wants to verify names and departments.

Write the query for that check.

#### 5. Wrong insert order

A student writes this query:

```sql
INSERT INTO Employee
VALUES ('Rahul Sharma', 101, 'IT', '2022-06-01', 'M', 'rahul@email.com');
```

Answer these:

1. What is wrong in this query?
2. Which rule of `INSERT` did they break?
3. How should the query be corrected?

#### 6. College admissions system

A college wants to store student records with these rules:

* each student must have a unique ID
* the full name can store up to 120 characters
* the course name can store up to 60 characters
* the admission date should store only the date

Write the query to create this table.

### Challenge questions

1. Create a table named `Books` with `BookID`, `BookName`, `AuthorName`, and `Price`.
2. Insert four books in a single query.
3. Show only `BookName` and `Price` from the table.
4. Create another version of the `Books` table where `BookID` uses `IDENTITY(500,5)`.

{% hint style="success" %}
If you can solve these without looking back at the notes, you are ready for the next SQL topic.
{% endhint %}
