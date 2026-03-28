---
description: we will create our first database and insert data inside our database
hidden: true
---

# Database Creation

## Creating Your First Database and Table

Now that we understand data types, let's put it all into practice. We are going to create a database called console\_db, and inside it, we'll create a table called Employee.

### Step 1: Create the Database

First, we need to create a database. A database is like a container that will hold all our tables.

```sql
---SYNTAX :
---CREATE DATABASE <DATABASE_NAME>;

   CREATE DATABASE console_db;
```

### Step 2: Use the Database

Before we can create tables inside the database, we need to tell SQL Server which database we want to work in. We do this with the **USE** command:

```sql
---SYNTAX :-
---USE <DATABASE_NAME>;

   USE console_db;
```

Now, any table we create will be created inside console\_db.

### Step 3: Create the Employee Table

Now we create the Employee table with the following columns:

• ID  :  a unique identifier for each employee

• FullName  :  the employee's full name

• Department  :  which department they work in

• DateOfJoining  : the date they joined the company

• Gender  :  M or F

• EmailID  :  their email address

Here is the SQL code to create this table:

```sql
CREATE TABLE Employee (
    ID INT PRIMARY KEY,
    FullName VARCHAR(100),
    Department VARCHAR(50),
    DateOfJoining DATE,
    Gender CHAR(1),
    EmailID VARCHAR(150)
);

```

Let's break this down line by line:

**1.     CREATE TABLE Employee -> we are creating a new table and naming it Employee**

**2.     ID INT PRIMARY KEY -> ID is a whole number (INT) and it is the primary key (more on this in a moment)**

**3.     FullName VARCHAR(100) -> FullName stores text up to 100 characters**

**4.     Department VARCHAR(50) -> Department stores text up to 50 characters**

**5.     DateOfJoining DATE -> stores only the date**

**6.     Gender CHAR(1) -> stores exactly 1 character (M or F)**

**7.     EmailID VARCHAR(150) -> stores email addresses up to 150 characters**

#### What is a Primary Key?

You may have noticed we marked ID as PRIMARY KEY. This is extremely important.

A primary key is a column (or combination of columns) that uniquely identifies each row in a table. No two rows can have the same primary key value, and the primary key can never be empty (NULL).

> &#x20;Real-Life Example
>
> In the Employee table:
>
> &#x20; • Employee 1 has ID = 101
>
> &#x20; • Employee 2 has ID = 102
>
> &#x20; • Employee 3 has ID = 103
>
> &#x20;
>
> Every employee gets a unique ID. Even if two employees have the same name, same department, same everything — their IDs will always be different.
>
> &#x20;
>
> This is how we tell rows apart and reference them without confusion.
>
>
>
> #### **Rules of a Primary Key:**
>
> &#x20;**1. Must be unique — no two rows can share the same primary key value**
>
> &#x20; **2. Cannot be NULL — every row must have a value in the primary key column**
>
> &#x20; **3. Should never change — once assigned, the primary key value should stay the same for that row**

### Using SELECT to Retrieve Data

Now that we have a table, let's learn how to read data from it. The command we use is SELECT.

Right now, our Employee table is empty , we haven't added any data yet. But let's learn the SELECT command first, and then we'll insert data and see it in action.

**Basic SELECT Syntax**

The most basic form of SELECT is:

<table data-header-hidden><thead><tr><th valign="top"></th></tr></thead><tbody><tr><td valign="top">SELECT * FROM Employee;</td></tr></tbody></table>

Let's break it down:

• SELECT  ->  tells SQL Server we want to retrieve data

• \*  ->   means 'all columns'. The asterisk is used to select everything.

• FROM Employee  ->  tells SQL Server which table to get the data from

So this query means: 'Show me all columns from all rows in the Employee table.'

#### Selecting Specific Columns

What if you don't want all columns,only specific ones? You can specify exactly which columns you want:

<table data-header-hidden><thead><tr><th valign="top"></th></tr></thead><tbody><tr><td valign="top">SELECT FullName, Department FROM Employee;</td></tr></tbody></table>

This query will show only the FullName and Department columns,it will ignore ID, DateOfJoining, Gender, and EmailID.

### Using INSERT to Add Data

Now let's actually put some data into the table. We use the INSERT command to add new rows.

#### Inserting a Single Row

Here is how you add one employee to the table:

```sql
INSERT INTO Employee (ID, FullName, Department, DateOfJoining, Gender, EmailID)
VALUES (101, 'Ravi Sharma', 'Sales', '2022-05-15', 'M', 'ravi.sharma@company.com');
```

Let's break this down:

1\.     INSERT INTO Employee -> we are inserting data into the Employee table

2\.     (ID, FullName, Department, DateOfJoining, Gender, EmailID) -> these are the column names we are providing values for

3\.     VALUES (101, 'Ravi Sharma', 'Sales', '2022-05-15', 'M', 'ravi.sharma@company.com') ->  these are the actual values, in the same order as the column names

| Important rules:                                                                                                                                                                                                                                                     |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>  • Text values must be in single quotes: 'Ravi Sharma'</p><p>  • Numbers do not need quotes: 101</p><p>  • Dates must be in single quotes and in the format 'YYYY-MM-DD': '2022-05-15'</p><p>  • The values must match the order of the column names exactly</p> |

### Inserting Multiple Rows at Once

**You can simply provide the values in the exact order that the columns appear in the table.**

```sql
INSERT INTO Employee
VALUES 
(106, 'Neha Desai', 'IT', '2022-09-18', 'F', 'neha.desai@company.com'),
(107, 'Rajesh Iyer', 'HR', '2021-12-03', 'M', 'rajesh.iyer@company.com'),
(108, 'Kavita Rao', 'Sales', '2023-02-20', 'F', 'kavita.rao@company.com');
```

### Important Rules When Using This Method

**1. You MUST provide values for ALL columns**

* If your table has 6 columns, you must provide exactly 6 values
* You cannot skip any column

**2. The values MUST be in the exact same order as the columns in the table**

* Our Employee table has columns in this order: ID, FullName, Department, DateOfJoining, Gender, EmailID
* So values must be provided in exactly that order

**3. If you get the order wrong, data goes into the wrong columns**

* This can cause serious errors or put wrong data in wrong places

#### What Happens If You Try to Insert a Duplicate Primary Key?

Let's test what happens if we try to insert another employee with ID = 101 (which Ravi already has):

```sql
INSERT INTO Employee (ID, FullName, Department, DateOfJoining, Gender, EmailID)
VALUES (101, 'Another Person', 'Finance', '2023-06-01', 'M', 'another@company.com');
```

If you run this, SQL Server will give you an error:

> 'Violation of PRIMARY KEY constraint... Cannot insert duplicate key.'

This is exactly what we want! The primary key is doing its job , protecting the data from duplicates.

