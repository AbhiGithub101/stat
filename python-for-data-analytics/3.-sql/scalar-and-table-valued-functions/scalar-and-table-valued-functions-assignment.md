# Scalar & Table Valued Functions Assignment

### Practice dataset

```sql
CREATE TABLE EmployeeFunctionPractice (
    EmployeeID INT PRIMARY KEY,
    FullName VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10, 2),
    City VARCHAR(50)
);

INSERT INTO EmployeeFunctionPractice
    (EmployeeID, FullName, Department, Salary, City)
VALUES
    (1, 'Rahul Sharma', 'IT', 50000.00, 'Delhi'),
    (2, 'Priya Verma', 'HR', 45000.00, 'Mumbai'),
    (3, 'Amit Gupta', 'Finance', 60000.00, 'Delhi'),
    (4, 'Sneha Patil', 'IT', 55000.00, 'Pune'),
    (5, 'Ravi Shankar', 'HR', 48000.00, 'Mumbai'),
    (6, 'Neha Singh', 'Finance', 70000.00, 'Delhi'),
    (7, 'Arjun Mehta', 'IT', 42000.00, 'Pune'),
    (8, 'Kavya Reddy', 'HR', 65000.00, 'Hyderabad');
```

### Scalar functions

#### 1. What does a scalar function return?(makethisquestion mcq)

<details>

<summary>Solution</summary>

A scalar function returns **one value**. The value can be text, a number, or a date.

</details>

#### 2. Which statement creates a scalar function in SQL Server?

* A. `CREATE PROCEDURE`
* B. `CREATE FUNCTION`
* C. `CREATE TABLE`
* D. `CREATE VIEW`

<details>

<summary>Solution</summary>

**B. `CREATE FUNCTION`**

</details>

#### 3. Create `fn_PracticeTax`. It must return 10% tax for a salary.

<details>

<summary>Solution</summary>

```sql
CREATE FUNCTION fn_PracticeTax (@Salary DECIMAL(10, 2))
RETURNS DECIMAL(10, 2)
AS
BEGIN
    DECLARE @Tax DECIMAL(10, 2);
    SET @Tax = @Salary * 0.10;
    RETURN @Tax;
END;
```

</details>

#### 4. Call `fn_PracticeTax` for the value `50000`. Display the result as `TaxAmount`.

<details>

<summary>Solution</summary>

```sql
SELECT dbo.fn_PracticeTax(50000) AS TaxAmount;
```

The `dbo.` schema name is used when calling the function.

</details>

#### 5. Complete the missing keyword.

```sql
CREATE FUNCTION fn_Square (@Number INT)
RETURNS INT
AS
BEGIN
    _____ @Number * @Number;
END;
```

<details>

<summary>Solution</summary>

```sql
RETURN @Number * @Number;
```

`RETURN` sends one value back from a scalar function.

</details>

#### 6. Display each employee’s name, salary, and tax. Use `fn_PracticeTax` with the `Salary` column.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       Salary,
       dbo.fn_PracticeTax(Salary) AS TaxAmount
FROM EmployeeFunctionPractice;
```

</details>

#### 7. Create `fn_PracticeNetSalary`. It must accept a salary and return the salary after 10% tax.

<details>

<summary>Solution</summary>

```sql
CREATE FUNCTION fn_PracticeNetSalary (@Salary DECIMAL(10, 2))
RETURNS DECIMAL(10, 2)
AS
BEGIN
    DECLARE @NetSalary DECIMAL(10, 2);
    SET @NetSalary = @Salary - (@Salary * 0.10);
    RETURN @NetSalary;
END;
```

</details>

#### 8. A function needs both salary and bonus percentage. Create `fn_PracticeSalaryAfterBonus` to return the final salary.

<details>

<summary>Solution</summary>

```sql
CREATE FUNCTION fn_PracticeSalaryAfterBonus
    (@Salary DECIMAL(10, 2), @BonusPercent DECIMAL(5, 2))
RETURNS DECIMAL(10, 2)
AS
BEGIN
    DECLARE @FinalSalary DECIMAL(10, 2);
    SET @FinalSalary = @Salary + (@Salary * @BonusPercent / 100);
    RETURN @FinalSalary;
END;
```

</details>

#### 9. Display the name, current salary, and salary after a 15% bonus. Use `fn_PracticeSalaryAfterBonus`.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       Salary,
       dbo.fn_PracticeSalaryAfterBonus(Salary, 15) AS SalaryAfterBonus
FROM EmployeeFunctionPractice;
```

</details>

#### 10. Change `fn_PracticeTax` so it returns 20% tax.

<details>

<summary>Solution</summary>

```sql
ALTER FUNCTION fn_PracticeTax (@Salary DECIMAL(10, 2))
RETURNS DECIMAL(10, 2)
AS
BEGIN
    DECLARE @Tax DECIMAL(10, 2);
    SET @Tax = @Salary * 0.20;
    RETURN @Tax;
END;
```

`ALTER FUNCTION` changes an existing function.

</details>

#### 11. True or False: A scalar function can return a complete result table.

<details>

<summary>Solution</summary>

**False.**

A scalar function returns one value. A table-valued function returns rows and columns.

</details>

#### 12. Write the statement that removes `fn_PracticeNetSalary`.

<details>

<summary>Solution</summary>

```sql
DROP FUNCTION fn_PracticeNetSalary;
```

</details>

### Inline table-valued functions

#### 13. What does an inline table-valued function return?(can be mca ques)

<details>

<summary>Solution</summary>

It returns a **table** from one `SELECT` statement.

</details>

#### 14. Which syntax belongs to an inline table-valued function?

* A. `RETURNS INT`
* B. `RETURNS TABLE AS RETURN (SELECT ...)`
* C. `RETURNS @Result TABLE AS BEGIN`
* D. `RETURN @Value`

<details>

<summary>Solution</summary>

**B. `RETURNS TABLE AS RETURN (SELECT ...)`**

</details>

#### 15. Create `fn_PracticeEmployeesByDept`. It must return employees for the supplied department.

<details>

<summary>Solution</summary>

```sql
CREATE FUNCTION fn_PracticeEmployeesByDept (@Department VARCHAR(50))
RETURNS TABLE
AS
RETURN
(
    SELECT EmployeeID, FullName, Department, Salary, City
    FROM EmployeeFunctionPractice
    WHERE Department = @Department
);
```

</details>

#### 16. Return every employee from the IT department using `fn_PracticeEmployeesByDept`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM dbo.fn_PracticeEmployeesByDept('IT');
```

A TVF is used in the `FROM` clause like a table.

</details>

#### 17. Fill in the blank to define an inline TVF result.

```sql
CREATE FUNCTION fn_DepartmentList (@Department VARCHAR(50))
RETURNS TABLE
AS
_____ 
(
    SELECT FullName
    FROM EmployeeFunctionPractice
    WHERE Department = @Department
);
```

<details>

<summary>Solution</summary>

```sql
RETURN
```

</details>

#### 18. Create `fn_PracticeHighEarners`. It must return employee ID, name, department, and salary above a supplied minimum salary.

<details>

<summary>Solution</summary>

```sql
CREATE FUNCTION fn_PracticeHighEarners (@MinSalary DECIMAL(10, 2))
RETURNS TABLE
AS
RETURN
(
    SELECT EmployeeID, FullName, Department, Salary
    FROM EmployeeFunctionPractice
    WHERE Salary > @MinSalary
);
```

</details>

#### 19. Use `fn_PracticeHighEarners` to show employees earning above `55000`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM dbo.fn_PracticeHighEarners(55000);
```

</details>

#### 20. Show IT employees from `fn_PracticeEmployeesByDept` in salary order, highest first.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM dbo.fn_PracticeEmployeesByDept('IT')
ORDER BY Salary DESC;
```

</details>

#### 21. Return Delhi employees earning above `50000`. Start with `fn_PracticeHighEarners`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM dbo.fn_PracticeHighEarners(50000)
WHERE City = 'Delhi';
```

The TVF result can be filtered further.

</details>

#### 22. True or False: An inline TVF uses `BEGIN` and `END` around its query.

<details>

<summary>Solution</summary>

**False.**

An inline TVF uses `RETURN` followed by one query.

</details>

#### 23. Alter `fn_PracticeEmployeesByDept` to return only employees with salary above `45000`.

<details>

<summary>Solution</summary>

```sql
ALTER FUNCTION fn_PracticeEmployeesByDept (@Department VARCHAR(50))
RETURNS TABLE
AS
RETURN
(
    SELECT EmployeeID, FullName, Department, Salary, City
    FROM EmployeeFunctionPractice
    WHERE Department = @Department
      AND Salary > 45000
);
```

</details>

### Multi-statement table-valued functions

#### 24. Which return declaration is valid for a multi-statement TVF?

* A. `RETURNS DECIMAL(10, 2)`
* B. `RETURNS TABLE`
* C. `RETURNS @CityStats TABLE (...)`
* D. `RETURN @CityStats`

<details>

<summary>Solution</summary>

**C. `RETURNS @CityStats TABLE (...)`**

</details>

#### 25. Create `fn_PracticeCityReport`. It must return city, employee count, average salary, and highest salary.

<details>

<summary>Solution</summary>

```sql
CREATE FUNCTION fn_PracticeCityReport ()
RETURNS @CityStats TABLE
(
    City VARCHAR(50),
    TotalEmployees INT,
    AverageSalary DECIMAL(10, 2),
    HighestSalary DECIMAL(10, 2)
)
AS
BEGIN
    INSERT INTO @CityStats
        (City, TotalEmployees, AverageSalary, HighestSalary)
    SELECT City,
           COUNT(*),
           AVG(Salary),
           MAX(Salary)
    FROM EmployeeFunctionPractice
    GROUP BY City;

    RETURN;
END;
```

</details>

#### 26. Display the result of `fn_PracticeCityReport`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM dbo.fn_PracticeCityReport();
```

</details>

#### 27. Complete the missing statement.

```sql
CREATE FUNCTION fn_Example ()
RETURNS @Result TABLE (EmployeeID INT)
AS
BEGIN
    INSERT INTO @Result
    SELECT EmployeeID
    FROM EmployeeFunctionPractice;

    _____;
END;
```

<details>

<summary>Solution</summary>

```sql
RETURN;
```

A multi-statement TVF ends with `RETURN;` without a value.

</details>

#### 28. Create `fn_PracticeDepartmentReport`. It must return each department, its employee count, and average salary.

<details>

<summary>Solution</summary>

```sql
CREATE FUNCTION fn_PracticeDepartmentReport ()
RETURNS @DepartmentStats TABLE
(
    Department VARCHAR(50),
    TotalEmployees INT,
    AverageSalary DECIMAL(10, 2)
)
AS
BEGIN
    INSERT INTO @DepartmentStats
        (Department, TotalEmployees, AverageSalary)
    SELECT Department,
           COUNT(*),
           AVG(Salary)
    FROM EmployeeFunctionPractice
    GROUP BY Department;

    RETURN;
END;
```

</details>

#### 29. Return the department report ordered by average salary, highest first.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM dbo.fn_PracticeDepartmentReport()
ORDER BY AverageSalary DESC;
```

</details>

#### 30. Create `fn_PracticeCityEmployees`. It must accept a city and return employee ID, name, department, and salary for that city. Use a multi-statement TVF.

<details>

<summary>Solution</summary>

```sql
CREATE FUNCTION fn_PracticeCityEmployees (@City VARCHAR(50))
RETURNS @CityEmployees TABLE
(
    EmployeeID INT,
    FullName VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10, 2)
)
AS
BEGIN
    INSERT INTO @CityEmployees
        (EmployeeID, FullName, Department, Salary)
    SELECT EmployeeID, FullName, Department, Salary
    FROM EmployeeFunctionPractice
    WHERE City = @City;

    RETURN;
END;
```

</details>

#### 31. Use `fn_PracticeCityEmployees` to display employees in Delhi.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM dbo.fn_PracticeCityEmployees('Delhi');
```

</details>

#### 32. True or False: A multi-statement TVF defines its output columns inside `RETURNS`.

<details>

<summary>Solution</summary>

**True.**

The table variable and its columns are declared after `RETURNS`.

</details>

#### 33. Add a `LowestSalary` column to `fn_PracticeCityReport`. Populate it for every city.

<details>

<summary>Solution</summary>

```sql
ALTER FUNCTION fn_PracticeCityReport ()
RETURNS @CityStats TABLE
(
    City VARCHAR(50),
    TotalEmployees INT,
    AverageSalary DECIMAL(10, 2),
    HighestSalary DECIMAL(10, 2),
    LowestSalary DECIMAL(10, 2)
)
AS
BEGIN
    INSERT INTO @CityStats
        (City, TotalEmployees, AverageSalary, HighestSalary, LowestSalary)
    SELECT City,
           COUNT(*),
           AVG(Salary),
           MAX(Salary),
           MIN(Salary)
    FROM EmployeeFunctionPractice
    GROUP BY City;

    RETURN;
END;
```

</details>

#### 34. Which function type best fits one `SELECT` statement with known output columns?

* A. Scalar function
* B. Inline TVF
* C. Multi-statement TVF
* D. Table variable

<details>

<summary>Solution</summary>

**B. Inline TVF**

It returns a table from one `SELECT` statement.

</details>

#### 35. Which function type best fits a report built by inserting rows into a returned table variable?

<details>

<summary>Solution</summary>

A **multi-statement table-valued function** fits this requirement.

</details>

#### 36. Remove `fn_PracticeCityEmployees`.

<details>

<summary>Solution</summary>

```sql
DROP FUNCTION fn_PracticeCityEmployees;
```

</details>
