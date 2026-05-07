# Scalar & Table Valued Functions

## What is a Function?

A Function is a **saved block of SQL code** that takes some input, does something with it, and gives back a result.

Think of it like a **juice machine** :

* You put in fruit (input)
* Machine processes it
* You get juice (output)

Every time you want juice ,you just put fruit in. You do not rebuild the machine each time. Same way  you write a function once, call it anytime.

## Types of Functions in SQL Server:

```
                    Functions
                        │
          ┌─────────────┴──────────────┐
          │                            │
   Scalar Function            Table Valued Function
   (returns ONE value)        (returns a TABLE)
                                        │
                          ┌─────────────┴──────────────┐
                          │                             │
               Inline TVF                  Multi-Statement TVF
          (columns known —            (columns unknown —
           single SELECT)              multiple statements)
```

#### Our Simple Table for Examples:

```sql
CREATE TABLE Employee (
    ID         INT PRIMARY KEY,
    FullName   VARCHAR(100),
    Department VARCHAR(50),
    Salary     DECIMAL(10,2),
    City       VARCHAR(50)
);

INSERT INTO Employee VALUES (1, 'Rahul Sharma',  'IT',      50000, 'Delhi');
INSERT INTO Employee VALUES (2, 'Priya Verma',   'HR',      45000, 'Mumbai');
INSERT INTO Employee VALUES (3, 'Amit Gupta',    'Finance', 60000, 'Delhi');
INSERT INTO Employee VALUES (4, 'Sneha Patil',   'IT',      55000, 'Pune');
INSERT INTO Employee VALUES (5, 'Ravi Shankar',  'HR',      48000, 'Mumbai');
INSERT INTO Employee VALUES (6, 'Neha Singh',    'Finance', 70000, 'Delhi');
INSERT INTO Employee VALUES (7, 'Arjun Mehta',   'IT',      42000, 'Pune');
INSERT INTO Employee VALUES (8, 'Kavya Reddy',   'HR',      65000, 'Hyderabad');
```

### SCALAR FUNCTIONS

A Scalar Function takes one or more inputs and **returns a single value** ,one number, one text, one date etc.

Think of it like a **calculator** :

* You give it numbers
* It returns one answer

┌─────────────────────────────────────\
│ SCALAR FUNCTION                                                           │              \
│                                                                                              │\
│ Input: Salary = 50000                                                        │\
│                   ↓                                                                        │\
│ Logic: Calculate tax                                                            │\
│ Tax = Salary \* 0.1                                                                │\
│                   ↓                                                                        │\
│ Output: 5000 (single value)                                               │\
└─────────────────────────────────────┘

#### Syntax : Creating a Scalar Function:

```sql
CREATE FUNCTION FunctionName (@Parameter DataType)
RETURNS ReturnDataType
AS
BEGIN
    -- your logic here
    DECLARE @Result DataType;
    SET @Result = -- calculation

    RETURN @Result;
END;
```

Breaking it down:

| Part                  | Meaning                        |
| --------------------- | ------------------------------ |
| `CREATE FUNCTION`     | Creates the function           |
| `FunctionName`        | Name you give the function     |
| `@Parameter DataType` | Input you pass to the function |
| `RETURNS DataType`    | What data type it will return  |
| `AS BEGIN...END`      | The logic block                |
| `RETURN`              | The value to send back         |

#### Example 1 : Calculate Tax on Salary:

```sql
CREATE FUNCTION fn_CalculateTax (@Salary DECIMAL(10,2))
RETURNS DECIMAL(10,2)
AS
BEGIN
    DECLARE @Tax DECIMAL(10,2);
    SET @Tax = @Salary * 0.10; -- 10% tax
    RETURN @Tax;
END;
```

#### Calling a Scalar Function:

> In SQL Server , always use schema name `dbo.` before function name when calling it.

```sql
-- Call with a direct value
SELECT dbo.fn_CalculateTax(50000) AS TaxAmount;
-- Output: 5000.00

-- Call with a column
SELECT FullName,
       Salary,
       dbo.fn_CalculateTax(Salary) AS TaxAmount
FROM Employee;
```

**Result:**

| FullName     | Salary | TaxAmount |
| ------------ | ------ | --------- |
| Rahul Sharma | 50000  | 5000.00   |
| Priya Verma  | 45000  | 4500.00   |
| Amit Gupta   | 60000  | 6000.00   |
| Sneha Patil  | 55000  | 5500.00   |
| Ravi Shankar | 48000  | 4800.00   |
| Neha Singh   | 70000  | 7000.00   |
| Arjun Mehta  | 42000  | 4200.00   |
| Kavya Reddy  | 65000  | 6500.00   |

#### Example 2 : Calculate Net Salary after tax:

```sql
CREATE FUNCTION fn_NetSalary (@Salary DECIMAL(10,2))
RETURNS DECIMAL(10,2)
AS
BEGIN
    DECLARE @NetSalary DECIMAL(10,2);
    SET @NetSalary = @Salary - (@Salary * 0.10);
    RETURN @NetSalary;
END;
```

**Calling it:**

```sql
SELECT FullName,
       Salary,
       dbo.fn_NetSalary(Salary) AS NetSalary
FROM Employee;
```

**Result:**

| FullName     | Salary | NetSalary |
| ------------ | ------ | --------- |
| Rahul Sharma | 50000  | 45000.00  |
| Priya Verma  | 45000  | 40500.00  |
| Amit Gupta   | 60000  | 54000.00  |
| Neha Singh   | 70000  | 63000.00  |
| Kavya Reddy  | 65000  | 58500.00  |

#### Example 3 : Function with multiple parameters:

```sql
CREATE FUNCTION fn_SalaryAfterBonus
    (@Salary DECIMAL(10,2), @BonusPercent DECIMAL(5,2))
RETURNS DECIMAL(10,2)
AS
BEGIN
    DECLARE @FinalSalary DECIMAL(10,2);
    SET @FinalSalary = @Salary + (@Salary * @BonusPercent / 100);
    RETURN @FinalSalary;
END;
```

**Calling it:**

```sql
SELECT FullName,
       Salary,
       dbo.fn_SalaryAfterBonus(Salary, 15) AS SalaryWith15PercentBonus
FROM Employee;
```

**Result:**

| FullName     | Salary | SalaryWith15PercentBonus |
| ------------ | ------ | ------------------------ |
| Rahul Sharma | 50000  | 57500.00                 |
| Priya Verma  | 45000  | 51750.00                 |
| Amit Gupta   | 60000  | 69000.00                 |
| Neha Singh   | 70000  | 80500.00                 |

#### Altering a Scalar Function:

Used to **modify** an existing function without dropping it:

```sql
ALTER FUNCTION fn_CalculateTax (@Salary DECIMAL(10,2))
RETURNS DECIMAL(10,2)
AS
BEGIN
    DECLARE @Tax DECIMAL(10,2);
    SET @Tax = @Salary * 0.20; -- changed from 10% to 20%
    RETURN @Tax;
END;
```

#### Dropping a Scalar Function:

```sql
DROP FUNCTION fn_CalculateTax;
DROP FUNCTION fn_NetSalary;
```

### TABLE VALUED FUNCTIONS (TVF)

A Table Valued Function returns a **whole table** instead of a single value ,you can SELECT from it just like a normal table.

Think of it like a **filter machine** :

* You give it a filter condition (input)
* It returns a whole filtered table (output)

───────────────────────────────────── ┐\
│ TABLE VALUED FUNCTION                                              │\
│                                                                                             │\
│ Input: Department = 'IT'                                                    │\
│                          ↓                                                                │\
│ Logic: Filter employees                                                     │\
│                          ↓                                                                │\
│ Output: Returns a TABLE                                                  │\
│ ┌──────────────────────────┐                    │\
│ │ ID │ Name  │ Dept │ Sal                          │                    │\
│ │ 1   │ Rahul  │ IT      │50000                     │                     │\
│ │ 4  │ Sneha │ IT      │55000                     │                     │\
│ │ 7  │ Arjun   │ IT      │42000                     │                     │\
│ └──────────────────────────┘                      │\
└─────────────────────────────────────┘

### Types of Table Valued Functions:

| Type                    |
| ----------------------- |
| **Inline TVF**          |
| **Multi-Statement TVF** |

#### Inline Table Valued Function:

**(Number of Columns KNOWN)**

Used when your output columns are **already known** and you need just one SELECT statement to get the result.

Think of it like a **saved filter** ,you know exactly what columns you want, just filter the data differently each time.

**Syntax:**

```sql
CREATE FUNCTION FunctionName (@Parameter DataType)
RETURNS TABLE
AS
RETURN
(
    SELECT columns
    FROM table
    WHERE condition
);
```

> Notice -> no BEGIN...END needed for Inline TVF. Just RETURN with a SELECT.

**Example 1 : Get all employees from a specific department:**

```sql
CREATE FUNCTION fn_GetEmployeesByDept (@Dept VARCHAR(50))
RETURNS TABLE
AS
RETURN
(
    SELECT ID, FullName, Department, Salary, City
    FROM Employee
    WHERE Department = @Dept
);
```

**Calling it ,use it like a table:**

```sql
SELECT * FROM dbo.fn_GetEmployeesByDept('IT');
```

**Result:**

| ID | FullName     | Department | Salary | City  |
| -- | ------------ | ---------- | ------ | ----- |
| 1  | Rahul Sharma | IT         | 50000  | Delhi |
| 4  | Sneha Patil  | IT         | 55000  | Pune  |
| 7  | Arjun Mehta  | IT         | 42000  | Pune  |

```sql
SELECT * FROM dbo.fn_GetEmployeesByDept('HR');
```

**Result:**

| ID | FullName     | Department | Salary | City      |
| -- | ------------ | ---------- | ------ | --------- |
| 2  | Priya Verma  | HR         | 45000  | Mumbai    |
| 5  | Ravi Shankar | HR         | 48000  | Mumbai    |
| 8  | Kavya Reddy  | HR         | 65000  | Hyderabad |

**Example 2 : Get employees above a salary:**

```sql
CREATE FUNCTION fn_GetHighEarners (@MinSalary DECIMAL(10,2))
RETURNS TABLE
AS
RETURN
(
    SELECT ID, FullName, Department, Salary
    FROM Employee
    WHERE Salary > @MinSalary
);
```

**Calling it:**

```sql
SELECT * FROM dbo.fn_GetHighEarners(55000);
```

**Result:**

| ID | FullName    | Department | Salary |
| -- | ----------- | ---------- | ------ |
| 3  | Amit Gupta  | Finance    | 60000  |
| 6  | Neha Singh  | Finance    | 70000  |
| 8  | Kavya Reddy | HR         | 65000  |

**You can also filter, sort and join on top of a TVF:**

```sql
-- Sort the result
SELECT * FROM dbo.fn_GetEmployeesByDept('IT')
ORDER BY Salary DESC;

-- Filter the result further
SELECT * FROM dbo.fn_GetHighEarners(50000)
WHERE City = 'Delhi';
```

#### Multi-Statement Table Valued Function

**(Number of Columns UNKNOWN / Complex Logic)**

Used when your output needs **multiple SQL statements** like declaring variables, using IF conditions, loops etc. before returning the result.

Here you **define the output table structure yourself** at the beginning then fill it using multiple statements.

Think of it like **building a custom report** :

* You first decide what columns the report will have
* Then you fill in the data using multiple steps

**Syntax:**

```sql
CREATE FUNCTION FunctionName (@Parameter DataType)
RETURNS @TableVariable TABLE
(
    Column1 DataType,
    Column2 DataType,
    ...
)
AS
BEGIN
    -- multiple statements to fill the table
    INSERT INTO @TableVariable
    SELECT ...

    -- more logic if needed

    RETURN; -- just RETURN, no value needed
END;
```

> Notice -> here you define the table structure inside RETURNS. And at the end just write RETURN with nothing after it.

**Example 1 :** **Get city wise employee count and average salary:**

```sql
CREATE FUNCTION fn_CityReport ()
RETURNS @CityStats TABLE
(
    City          VARCHAR(50),
    TotalEmployees INT,
    AverageSalary  DECIMAL(10,2),
    HighestSalary  DECIMAL(10,2)
)
AS
BEGIN
    INSERT INTO @CityStats (City, TotalEmployees, AverageSalary, HighestSalary)
    SELECT City,
           COUNT(*)       AS TotalEmployees,
           AVG(Salary)    AS AverageSalary,
           MAX(Salary)    AS HighestSalary
    FROM Employee
    GROUP BY City;

    RETURN;
END;
```

**Calling it:**

```sql
SELECT * FROM dbo.fn_CityReport();
```

**Result:**

| City      | TotalEmployees | AverageSalary | HighestSalary |
| --------- | -------------- | ------------- | ------------- |
| Delhi     | 3              | 60000         | 70000         |
| Mumbai    | 2              | 46500         | 48000         |
| Pune      | 2              | 48500         | 55000         |
| Hyderabad | 1              | 65000         | 65000         |

#### Altering a Table Valued Function:

```sql
ALTER FUNCTION fn_GetEmployeesByDept (@Dept VARCHAR(50))
RETURNS TABLE
AS
RETURN
(
    SELECT ID, FullName, Department, Salary
    FROM Employee
    WHERE Department = @Dept
    AND Salary > 45000  -- added extra condition
);
```

#### Dropping a Table Valued Function:

```sql
DROP FUNCTION fn_GetEmployeesByDept;
DROP FUNCTION fn_CityReport;
```

#### Scalar vs Table Valued :&#x20;

```
SCALAR FUNCTION              TABLE VALUED FUNCTION
┌─────────────────┐          ┌─────────────────────┐
│ Input: Salary   │          │ Input: Department   │
│       50000     │          │       'IT'          │
│        ↓        │          │        ↓            │
│ Logic: * 0.10   │          │ Logic: Filter rows  │
│        ↓        │          │        ↓            │
│ Output:         │          │ Output:             │
│   5000.00       │          │ ┌────────────────┐  │
│ (single value)  │          │ │ ID│Name│Salary │  │
└─────────────────┘          │ │ 1 │Rahul│50000 │  │
                             │ │ 4 │Sneha│55000 │  │
                             │ └────────────────┘  │
                             │ (whole table)       │
                             └─────────────────────┘
```

> **Up Next : We will cover what are constraints in SQL.**
