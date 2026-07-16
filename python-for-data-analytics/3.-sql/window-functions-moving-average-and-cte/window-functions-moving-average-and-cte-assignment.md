---
description: >-
  Practice SQL Server window functions, moving calculations, and CTEs with
  shared sample data.
hidden: true
---

# Window Functions, Moving Average & CTE Assignment

### Shared dataset

```sql
CREATE TABLE Employee (
    ID INT PRIMARY KEY,
    FullName VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2),
    City VARCHAR(50)
);

INSERT INTO Employee VALUES
(1, 'Rahul Sharma', 'IT', 50000, 'Delhi'),
(2, 'Priya Verma', 'HR', 45000, 'Mumbai'),
(3, 'Amit Gupta', 'Finance', 60000, 'Delhi'),
(4, 'Sneha Patil', 'IT', 55000, 'Pune'),
(5, 'Ravi Shankar', 'HR', 48000, 'Mumbai'),
(6, 'Neha Singh', 'Finance', 70000, 'Delhi'),
(7, 'Arjun Mehta', 'IT', 42000, 'Pune'),
(8, 'Kavya Reddy', 'HR', 65000, 'Hyderabad'),
(9, 'Vikram Das', 'Finance', 60000, 'Delhi'),
(10, 'Pooja Nair', 'IT', 55000, 'Mumbai');

CREATE TABLE DailySales (
    DayNumber INT,
    SaleAmount INT
);

INSERT INTO DailySales VALUES
(1, 100), (2, 200), (3, 150), (4, 300), (5, 250),
(6, 400), (7, 350), (8, 500), (9, 450), (10, 600);
```

### Window functions

#### 1. Show every employee with their department's average salary.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       Department,
       Salary,
       AVG(Salary) OVER (PARTITION BY Department) AS DeptAvgSalary
FROM Employee;
```

</details>

#### 2. The HR team needs one unique salary position for every employee. Show each employee with a salary row number, highest salary first.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       Department,
       Salary,
       ROW_NUMBER() OVER (ORDER BY Salary DESC) AS SalaryRowNumber
FROM Employee;
```

</details>

#### 3. Show each employee with their company salary rank. Equal salaries must share a rank.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       Salary,
       RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employee;
```

</details>

#### 4. Show each employee with their company dense salary rank. Equal salaries must share a rank without gaps.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       Salary,
       DENSE_RANK() OVER (ORDER BY Salary DESC) AS DenseSalaryRank
FROM Employee;
```

</details>

#### 5. Rank employees by salary inside each department. Show the employee name, department, salary, and rank.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       Department,
       Salary,
       RANK() OVER (
           PARTITION BY Department
           ORDER BY Salary DESC
       ) AS DepartmentSalaryRank
FROM Employee;
```

</details>

#### 6. Produce a payroll report that shows each employee and their department average. Return only employees earning above that displayed average.

<details>

<summary>Solution</summary>

```sql
WITH EmployeeSalary AS (
    SELECT FullName,
           Department,
           Salary,
           AVG(Salary) OVER (PARTITION BY Department) AS DeptAvgSalary
    FROM Employee
)
SELECT FullName,
       Department,
       Salary,
       DeptAvgSalary
FROM EmployeeSalary
WHERE Salary > DeptAvgSalary;
```

The CTE lets the outer query filter the calculated window value.

</details>

#### 7. Which function assigns a different sequential number to tied salaries?

A. `RANK()`\
B. `DENSE_RANK()`\
C. `ROW_NUMBER()`\
D. `AVG()`

<details>

<summary>Solution</summary>

**C. `ROW_NUMBER()`**

It assigns a unique number to every row.

</details>

#### 8. Fill in the blank: `PARTITION BY Department` calculates a window separately for each \_\_\_\_\_\_\_\_.

<details>

<summary>Solution</summary>

**department**

</details>

#### 9. True or False: `DENSE_RANK()` skips the next rank after a tie.

<details>

<summary>Solution</summary>

**False.** `RANK()` skips ranks after ties. `DENSE_RANK()` does not.

</details>

### Moving calculations

#### 10. Show daily sales with a three-day moving average.

<details>

<summary>Solution</summary>

```sql
SELECT DayNumber,
       SaleAmount,
       AVG(CAST(SaleAmount AS DECIMAL(10,2))) OVER (
           ORDER BY DayNumber
           ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
       ) AS MovingAvg3Days
FROM DailySales;
```

</details>

#### 11. Show daily sales with a running total from day 1.

<details>

<summary>Solution</summary>

```sql
SELECT DayNumber,
       SaleAmount,
       SUM(SaleAmount) OVER (
           ORDER BY DayNumber
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS RunningTotal
FROM DailySales;
```

</details>

#### 12. The store wants a two-day moving average. Show each day, its sale amount, and that average.

<details>

<summary>Solution</summary>

```sql
SELECT DayNumber,
       SaleAmount,
       AVG(CAST(SaleAmount AS DECIMAL(10,2))) OVER (
           ORDER BY DayNumber
           ROWS BETWEEN 1 PRECEDING AND CURRENT ROW
       ) AS MovingAvg2Days
FROM DailySales;
```

</details>

#### 13. Show each day with the sum of sales for that day and the two preceding days.

<details>

<summary>Solution</summary>

```sql
SELECT DayNumber,
       SaleAmount,
       SUM(SaleAmount) OVER (
           ORDER BY DayNumber
           ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
       ) AS MovingSum3Days
FROM DailySales;
```

</details>

#### 14. Return only days where the sale amount is greater than its three-day moving average.

<details>

<summary>Solution</summary>

```sql
WITH SalesAverage AS (
    SELECT DayNumber,
           SaleAmount,
           AVG(CAST(SaleAmount AS DECIMAL(10,2))) OVER (
               ORDER BY DayNumber
               ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
           ) AS MovingAvg3Days
    FROM DailySales
)
SELECT DayNumber,
       SaleAmount,
       MovingAvg3Days
FROM SalesAverage
WHERE SaleAmount > MovingAvg3Days;
```

</details>

#### 15. Which phrase starts a running-total window at the first row?

A. `CURRENT ROW`\
B. `2 PRECEDING`\
C. `UNBOUNDED PRECEDING`\
D. `PARTITION BY`

<details>

<summary>Solution</summary>

**C. `UNBOUNDED PRECEDING`**

</details>

#### 16. Fill in the blank: A three-row moving window uses `ROWS BETWEEN 2 PRECEDING AND ________`.

<details>

<summary>Solution</summary>

**CURRENT ROW**

</details>

#### 17. True or False: A three-day moving average always uses exactly three rows.

<details>

<summary>Solution</summary>

**False.** Early rows use only the rows available so far.

</details>

### Common table expressions

#### 18. Which keyword begins a CTE in SQL Server?

<details>

<summary>Solution</summary>

`WITH`

</details>

#### 19. Create a CTE named `DepartmentAverage` that returns each department and its average salary. Select all rows from it.

<details>

<summary>Solution</summary>

```sql
WITH DepartmentAverage AS (
    SELECT Department,
           AVG(Salary) AS AvgSalary
    FROM Employee
    GROUP BY Department
)
SELECT *
FROM DepartmentAverage;
```

</details>

#### 20. Use a CTE to show employees whose salary is above their department average.

<details>

<summary>Solution</summary>

```sql
WITH DepartmentAverage AS (
    SELECT Department,
           AVG(Salary) AS AvgSalary
    FROM Employee
    GROUP BY Department
)
SELECT E.FullName,
       E.Department,
       E.Salary,
       D.AvgSalary
FROM Employee AS E
JOIN DepartmentAverage AS D
    ON E.Department = D.Department
WHERE E.Salary > D.AvgSalary;
```

</details>

#### 21. Create a CTE that calculates each department's average salary. Then show only departments with an average salary above `55000`.

<details>

<summary>Solution</summary>

```sql
WITH DepartmentAverage AS (
    SELECT Department,
           AVG(Salary) AS AvgSalary
    FROM Employee
    GROUP BY Department
)
SELECT Department,
       AvgSalary
FROM DepartmentAverage
WHERE AvgSalary > 55000;
```

</details>

#### 22. Use a CTE to calculate a running sales total. Return only days where the running total exceeds `2000`.

<details>

<summary>Solution</summary>

```sql
WITH RunningSales AS (
    SELECT DayNumber,
           SaleAmount,
           SUM(SaleAmount) OVER (
               ORDER BY DayNumber
               ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
           ) AS RunningTotal
    FROM DailySales
)
SELECT DayNumber,
       SaleAmount,
       RunningTotal
FROM RunningSales
WHERE RunningTotal > 2000;
```

</details>

#### 23. Build a salary report using one CTE. Include each employee's department average and department salary rank. Return the highest-paid employee or employees from each department.

<details>

<summary>Solution</summary>

```sql
WITH DepartmentSalaryReport AS (
    SELECT FullName,
           Department,
           Salary,
           AVG(Salary) OVER (PARTITION BY Department) AS DeptAvgSalary,
           RANK() OVER (
               PARTITION BY Department
               ORDER BY Salary DESC
           ) AS DepartmentSalaryRank
    FROM Employee
)
SELECT FullName,
       Department,
       Salary,
       DeptAvgSalary,
       DepartmentSalaryRank
FROM DepartmentSalaryReport
WHERE DepartmentSalaryRank = 1;
```

`RANK()` returns every tied highest-paid employee.

</details>

#### 24. Where must the main query appear when using a CTE?

A. Before `WITH`\
B. Immediately after the CTE\
C. Inside `PARTITION BY`\
D. Inside `GROUP BY`

<details>

<summary>Solution</summary>

**B. Immediately after the CTE**

</details>

#### 25. Fill in the blank: `WITH SalesCTE AS (SELECT * FROM DailySales) SELECT * FROM ________;`

<details>

<summary>Solution</summary>

**SalesCTE**

</details>

#### 26. True or False: A CTE can make a calculated result easier to filter in an outer query.

<details>

<summary>Solution</summary>

**True.** The outer query can filter columns returned by the CTE.

</details>
