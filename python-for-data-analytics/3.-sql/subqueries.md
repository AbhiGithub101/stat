# SubQueries

A Subquery is simply a **SELECT query written inside another SELECT query.**

The inner query runs first gives its result and then the outer query uses that result.

Think of it like this:

You ask your friend _"Who is the tallest person in our class?" and_ Your friend first checks everyone's height and then tells you the name. You used your friend's answer to get your final answer.

That is exactly what a subquery does , **SQL answers one question first, then uses that answer to answer your main question**

#### Visual Diagram of how a Subquery works:

```
┌─────────────────────────────────────┐
│           OUTER QUERY               │
│                                     │
│   SELECT * FROM Employee            │
│   WHERE Salary >                    │
│              ┌──────────────────┐   │
│              │   INNER QUERY    │   │
│              │  (Subquery)      │   │
│              │                  │   │
│              │  SELECT AVG      │   │
│              │  (Salary) FROM   │   │
│              │  Employee        │   │
│              │                  │   │
│              │  Runs FIRST      │   │
│              │  Returns: 51600  │   │
│              └──────────────────┘   │
│                                     │
│   WHERE Salary > 51600              │
│   Now outer query runs              │
└─────────────────────────────────────┘
```

> Inner query runs first → gives result → outer query uses that result.

#### Our Simple Table for Examples

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

**Table looks like this:**

| ID | FullName     | Department | Salary | City      |
| -- | ------------ | ---------- | ------ | --------- |
| 1  | Rahul Sharma | IT         | 50000  | Delhi     |
| 2  | Priya Verma  | HR         | 45000  | Mumbai    |
| 3  | Amit Gupta   | Finance    | 60000  | Delhi     |
| 4  | Sneha Patil  | IT         | 55000  | Pune      |
| 5  | Ravi Shankar | HR         | 48000  | Mumbai    |
| 6  | Neha Singh   | Finance    | 70000  | Delhi     |
| 7  | Arjun Mehta  | IT         | 42000  | Pune      |
| 8  | Kavya Reddy  | HR         | 65000  | Hyderabad |

## Types of Subqueries

Subqueries can be used in three places:

| Where                    | Example                                     |
| ------------------------ | ------------------------------------------- |
| Inside **WHERE** clause  | Most common,filter based on subquery result |
| Inside **FROM** clause   | Use subquery result as a temporary table    |
| Inside **SELECT** clause | Calculate a value for each row              |

### 1. Subquery in WHERE Clause

This is the **most common** use of subqueries ,filter rows based on the result of another query.

Example 1 : Find employees who earn more than the average salary:

**Step 1 :** **First find the average salary:**

```sql
SELECT AVG(Salary) FROM Employee;
-- Output: 54375
```

**Step 2 :** **Now use that in the main query:**

```sql
SELECT * FROM Employee
WHERE Salary > 54375;
```

**The problem** is that you had to run two separate queries. What if the average changes tomorrow?

**The solution is Subquery:**

```sql
SELECT * FROM Employee
WHERE Salary > (SELECT AVG(Salary) FROM Employee);
```

**What happens:**

```
Inner query runs first:
SELECT AVG(Salary) FROM Employee
→ Returns: 54375

Outer query uses the result:
SELECT * FROM Employee
WHERE Salary > 54375
```

**Result:**

| ID | FullName    | Department | Salary | City      |
| -- | ----------- | ---------- | ------ | --------- |
| 3  | Amit Gupta  | Finance    | 60000  | Delhi     |
| 6  | Neha Singh  | Finance    | 70000  | Delhi     |
| 8  | Kavya Reddy | HR         | 65000  | Hyderabad |

> These three employees earn more than the average salary of 54375. And tomorrow if the average changes ,the subquery automatically recalculates. You never have to change the query.

**Example 2 : Find the highest paid employee:**

```sql
SELECT * FROM Employee
WHERE Salary = (SELECT MAX(Salary) FROM Employee);
```

**What happens:**

```
Inner query: SELECT MAX(Salary) FROM Employee
→ Returns: 70000

Outer query: SELECT * FROM Employee
WHERE Salary = 70000
```

**Result:**

| ID | FullName   | Department | Salary | City  |
| -- | ---------- | ---------- | ------ | ----- |
| 6  | Neha Singh | Finance    | 70000  | Delhi |

**Example 3 : Find employees who work in the same city as Rahul Sharma:**

```sql
SELECT * FROM Employee
WHERE City = (SELECT City FROM Employee WHERE FullName = 'Rahul Sharma');
```

**What happens:**

```
Inner query: SELECT City FROM Employee
             WHERE FullName = 'Rahul Sharma'
→ Returns: 'Delhi'

Outer query: SELECT * FROM Employee
             WHERE City = 'Delhi'
```

**Result:**

| ID | FullName     | Department | Salary | City  |
| -- | ------------ | ---------- | ------ | ----- |
| 1  | Rahul Sharma | IT         | 50000  | Delhi |
| 3  | Amit Gupta   | Finance    | 60000  | Delhi |
| 6  | Neha Singh   | Finance    | 70000  | Delhi |

**Example 4 :** **Using IN with Subquery:**

Find all employees who work in the same department as employees earning more than 60000:

```sql
SELECT * FROM Employee
WHERE Department IN (SELECT Department FROM Employee WHERE Salary > 60000);
```

**What happens:**

```
Inner query: SELECT Department FROM Employee
             WHERE Salary > 60000
→ Returns: 'Finance', 'HR'

Outer query: SELECT * FROM Employee
             WHERE Department IN ('Finance', 'HR')
```

**Result:**

| ID | FullName     | Department | Salary | City      |
| -- | ------------ | ---------- | ------ | --------- |
| 2  | Priya Verma  | HR         | 45000  | Mumbai    |
| 3  | Amit Gupta   | Finance    | 60000  | Delhi     |
| 5  | Ravi Shankar | HR         | 48000  | Mumbai    |
| 6  | Neha Singh   | Finance    | 70000  | Delhi     |
| 8  | Kavya Reddy  | HR         | 65000  | Hyderabad |

### 2. Subquery in FROM Clause

Here the subquery acts as a **temporary table** , you give it an alias and query from it just like a normal table.

Think of it like this: Instead of querying the original table directly ,you first create a mini summarized table and then query that.

**Visual Diagram:**

```
┌─────────────────────────────────────┐
│           OUTER QUERY               │
│                                     │
│   SELECT * FROM                     │
│              ┌──────────────────┐   │
│              │   SUBQUERY       │   │
│              │  (acts as a      │   │
│              │  temp table)     │   │
│              │                  │   │
│              │  SELECT dept,    │   │
│              │  AVG(Salary)     │   │
│              │  FROM Employee   │   │
│              │  GROUP BY dept   │   │
│              │                  │   │
│              │  Alias: DeptAvg  │   │
│              └──────────────────┘   │
│                                     │
│   WHERE DeptAvg.AvgSalary > 50000   │
└─────────────────────────────────────┘
```

**Example :** **Find departments where average salary is more than 50000:**

```sql
SELECT DeptAvg.Department, DeptAvg.AvgSalary
FROM (
    SELECT Department, AVG(Salary) AS AvgSalary
    FROM Employee
    GROUP BY Department
) AS DeptAvg
WHERE DeptAvg.AvgSalary > 50000;
```

**What happens:**

```
Inner query runs first — creates a temp table:

Department  | AvgSalary
IT          | 49000
HR          | 52666
Finance     | 65000

Outer query filters this temp table:
WHERE AvgSalary > 50000
```

**Result:**

| Department | AvgSalary |
| ---------- | --------- |
| HR         | 52666     |
| Finance    | 65000     |

### 3. Subquery in SELECT Clause

Here the subquery runs **for every single row** and returns one value per row ,like an extra calculated column.

**Example : Show each employee's salary and the overall average salary side by side:**

```sql
SELECT FullName,
       Salary,
       (SELECT AVG(Salary) FROM Employee) AS CompanyAverage
FROM Employee;
```

**Result:**

| FullName     | Salary | CompanyAverage |
| ------------ | ------ | -------------- |
| Rahul Sharma | 50000  | 54375          |
| Priya Verma  | 45000  | 54375          |
| Amit Gupta   | 60000  | 54375          |
| Sneha Patil  | 55000  | 54375          |
| Ravi Shankar | 48000  | 54375          |
| Neha Singh   | 70000  | 54375          |
| Arjun Mehta  | 42000  | 54375          |
| Kavya Reddy  | 65000  | 54375          |

> The subquery ran once and returned 54375  which appeared next to every row. Now you can easily see who is above and who is below average.

## Correlated vs Non-Correlated Subqueries

### **Non-Correlated Subquery**

The inner query runs **only once** completely independent of the outer query. The result is fixed and reused.

```sql
-- Inner query runs only once → returns 54375
-- That value is used for all rows
SELECT * FROM Employee
WHERE Salary > (SELECT AVG(Salary) FROM Employee);
```

```
Inner query: Runs ONCE → 54375
Outer query: Uses 54375 for every row comparison
```

### Correlated Subquery

The inner query runs **once for every row** of the outer query ,it depends on the outer query's current row.

Think of it like this: For each employee,go check something specific about that employee and return a result.

```sql
SELECT E1.FullName, E1.Department, E1.Salary
FROM Employee E1
WHERE E1.Salary > (
    SELECT AVG(E2.Salary)
    FROM Employee E2
    WHERE E2.Department = E1.Department
);
```

**What happens:**

```
For Rahul Sharma (IT, 50000):
  Inner query: AVG salary of IT department = 49000
  Is 50000 > 49000?  YES — include Rahul

For Priya Verma (HR, 45000):
  Inner query: AVG salary of HR department = 52666
  Is 45000 > 52666?  NO — exclude Priya

For Amit Gupta (Finance, 60000):
  Inner query: AVG salary of Finance = 65000
  Is 60000 > 65000?  NO — exclude Amit

...and so on for every row
```

**Result:**

| FullName     | Department | Salary |
| ------------ | ---------- | ------ |
| Rahul Sharma | IT         | 50000  |
| Sneha Patil  | IT         | 55000  |
| Kavya Reddy  | HR         | 65000  |
| Neha Singh   | Finance    | 70000  |

