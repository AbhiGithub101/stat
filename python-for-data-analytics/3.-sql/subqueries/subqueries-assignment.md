---
description: Practice SQL Server subqueries with one shared employee dataset
hidden: true
---

# SubQueries Assignment

### Practice dataset

```sql
CREATE TABLE Employee (
    ID INT PRIMARY KEY,
    FullName VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10, 2),
    City VARCHAR(50)
);

INSERT INTO Employee (ID, FullName, Department, Salary, City)
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

Use the `Employee` table for every question.

### Subqueries in the WHERE clause

#### 1. Which clause most commonly uses a subquery to filter rows?

* A. `WHERE`
* B. `ORDER BY`
* C. `CREATE TABLE`
* D. `INSERT INTO`

<details>

<summary>Solution</summary>

**A. `WHERE`**

A subquery in `WHERE` filters rows using another query result.

</details>

#### 2. Find every employee who earns more than the company average salary.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Employee
WHERE Salary > (
    SELECT AVG(Salary)
    FROM Employee
);
```

The inner query returns the company average salary.

</details>

#### 3. Complete the subquery that finds the highest salary.

```sql
SELECT *
FROM Employee
WHERE Salary = (
    SELECT ______(Salary)
    FROM Employee
);
```

<details>

<summary>Solution</summary>

```sql
MAX
```

The completed query is:

```sql
SELECT *
FROM Employee
WHERE Salary = (
    SELECT MAX(Salary)
    FROM Employee
);
```

</details>

#### 4. Find the employee with the highest salary.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Employee
WHERE Salary = (
    SELECT MAX(Salary)
    FROM Employee
);
```

The subquery returns the highest salary before the outer query runs.

</details>

#### 5. Find employees who work in the same city as Rahul Sharma.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Employee
WHERE City = (
    SELECT City
    FROM Employee
    WHERE FullName = 'Rahul Sharma'
);
```

The inner query returns Rahul Sharma's city.

</details>

### Using IN with a subquery

#### 6. `IN` checks whether a value matches one of the values returned by a subquery. True or False?

<details>

<summary>Solution</summary>

**True.**

`IN` compares a value with a list of values returned by the subquery.

</details>

#### 7. Which condition correctly finds departments returned by a subquery?

* A. `Department = (SELECT Department ...)`
* B. `Department IN (SELECT Department ...)`
* C. `Department AS (SELECT Department ...)`
* D. `Department FROM (SELECT Department ...)`

<details>

<summary>Solution</summary>

**B. `Department IN (SELECT Department ...)`**

`IN` supports multiple values returned by the subquery.

</details>

#### 8. Find all employees whose department has at least one employee earning more than `60000.00`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Employee
WHERE Department IN (
    SELECT Department
    FROM Employee
    WHERE Salary > 60000.00
);
```

The inner query returns the matching departments.

</details>

#### 9. Find all employees who work in cities where an employee earns more than `60000.00`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Employee
WHERE City IN (
    SELECT City
    FROM Employee
    WHERE Salary > 60000.00
);
```

The outer query returns every employee in the returned cities.

</details>

#### 10. Complete the missing keyword.

```sql
SELECT *
FROM Employee
WHERE Department _____ (
    SELECT Department
    FROM Employee
    WHERE Salary > 60000.00
);
```

<details>

<summary>Solution</summary>

```sql
IN
```

`IN` allows the outer query to compare against multiple departments.

</details>

### Subqueries in FROM and SELECT

#### 11. A subquery in the `FROM` clause needs an alias. True or False?

<details>

<summary>Solution</summary>

**True.**

Give the subquery an alias before using it in the outer query.

</details>

#### 12. Which alias is assigned to the subquery result?

```sql
SELECT DeptAvg.Department
FROM (
    SELECT Department, AVG(Salary) AS AvgSalary
    FROM Employee
    GROUP BY Department
) AS DeptAvg;
```

* A. `Employee`
* B. `Department`
* C. `DeptAvg`
* D. `AvgSalary`

<details>

<summary>Solution</summary>

**C. `DeptAvg`**

`DeptAvg` is the alias for the subquery result.

</details>

#### 13. Create a temporary department summary with department names and average salaries. Return only averages above `50000.00`.

<details>

<summary>Solution</summary>

```sql
SELECT DeptAvg.Department, DeptAvg.AvgSalary
FROM (
    SELECT Department, AVG(Salary) AS AvgSalary
    FROM Employee
    GROUP BY Department
) AS DeptAvg
WHERE DeptAvg.AvgSalary > 50000.00;
```

The inner query creates the department summary.

</details>

#### 14. Show each employee's name, salary, and the company average salary in one result.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       Salary,
       (
           SELECT AVG(Salary)
           FROM Employee
       ) AS CompanyAverage
FROM Employee;
```

The subquery value appears next to every employee row.

</details>

### Correlated and non-correlated subqueries

#### 15. Which subquery runs once for every row in the outer query?

* A. A non-correlated subquery
* B. A correlated subquery
* C. A `FROM` clause alias
* D. An aggregate function

<details>

<summary>Solution</summary>

**B. A correlated subquery**

It depends on values from the outer query's current row.

</details>

#### 16. A subquery that calculates the company average salary without using an outer-table alias is non-correlated. True or False?

<details>

<summary>Solution</summary>

**True.**

It runs independently and returns one company-wide average.

</details>

#### 17. Find employees who earn more than their own department average salary.

<details>

<summary>Solution</summary>

```sql
SELECT E1.FullName,
       E1.Department,
       E1.Salary
FROM Employee AS E1
WHERE E1.Salary > (
    SELECT AVG(E2.Salary)
    FROM Employee AS E2
    WHERE E2.Department = E1.Department
);
```

The inner query uses the outer employee's department.

</details>

#### 18. Complete the condition that connects the inner query to the outer query.

```sql
SELECT E1.FullName, E1.Department, E1.Salary
FROM Employee AS E1
WHERE E1.Salary > (
    SELECT AVG(E2.Salary)
    FROM Employee AS E2
    WHERE E2.Department = ______________
);
```

<details>

<summary>Solution</summary>

```sql
E1.Department
```

This reference makes the subquery correlated.

</details>

#### 19. Write a correlated subquery that returns employees whose salary is greater than the average salary in their city.

<details>

<summary>Solution</summary>

```sql
SELECT E1.FullName,
       E1.City,
       E1.Salary
FROM Employee AS E1
WHERE E1.Salary > (
    SELECT AVG(E2.Salary)
    FROM Employee AS E2
    WHERE E2.City = E1.City
);
```

The subquery calculates an average for each employee's city.

</details>
