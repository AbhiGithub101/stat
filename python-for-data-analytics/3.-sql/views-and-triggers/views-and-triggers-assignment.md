---
description: Practice SQL Server views and AFTER triggers with one shared employee dataset.
hidden: true
---

# Views and Triggers Assignment

### Practice dataset

```sql
CREATE TABLE Employee (
    ID INT PRIMARY KEY,
    FullName VARCHAR(100),
    Salary DECIMAL(10, 2)
);

CREATE TABLE Employee_Log (
    LogID INT IDENTITY(1,1),
    Action VARCHAR(50),
    EmployeeID INT,
    LogTime DATETIME DEFAULT GETDATE()
);

INSERT INTO Employee (ID, FullName, Salary)
VALUES
(1, 'Rahul Sharma', 50000.00),
(2, 'Priya Verma', 45000.00),
(3, 'Amit Gupta', 60000.00),
(4, 'Sneha Patil', 55000.00),
(5, 'Ravi Shankar', 48000.00);
```

### Views

#### 1. Create a view named `EmployeeDirectory`. Show `ID`, `FullName`, and `Salary` from `Employee`.

<details>

<summary>Solution</summary>

```sql
CREATE VIEW EmployeeDirectory AS
SELECT ID, FullName, Salary
FROM Employee;
```

</details>

#### 2. Which statement reads every row from a view named `EmployeeDirectory`?

* A. `OPEN EmployeeDirectory;`
* B. `SELECT * FROM EmployeeDirectory;`
* C. `EXECUTE EmployeeDirectory;`
* D. `SHOW EmployeeDirectory;`

<details>

<summary>Solution</summary>

**B. `SELECT * FROM EmployeeDirectory;`**

A view is queried like a table.

</details>

#### 3. Use `EmployeeDirectory` to show employees earning more than `50000`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM EmployeeDirectory
WHERE Salary > 50000;
```

</details>

#### 4. Complete the statement.

```sql
CREATE _____ HighSalaryEmployees AS
SELECT ID, FullName, Salary
FROM Employee
WHERE Salary >= 55000;
```

#### 5 Create `SalarySummary`. It must show the employee count, average salary, highest salary, and lowest salary.

<details>

<summary>Solution</summary>

```sql
CREATE VIEW SalarySummary AS
SELECT COUNT(*) AS EmployeeCount,
       AVG(Salary) AS AverageSalary,
       MAX(Salary) AS HighestSalary,
       MIN(Salary) AS LowestSalary
FROM Employee;
```

</details>

#### 6. A manager needs employees in descending salary order. Use `EmployeeDirectory`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM EmployeeDirectory
ORDER BY Salary DESC;
```

</details>

#### 7. Which statement changes the query stored in an existing view?

* A. `UPDATE VIEW`
* B. `MODIFY VIEW`
* C. `ALTER VIEW`
* D. `CHANGE VIEW`

<details>

<summary>Solution</summary>

**C. `ALTER VIEW`**

`ALTER VIEW` replaces the saved query definition.

</details>

#### 8. Alter `EmployeeDirectory` to show only `ID` and `FullName`.

<details>

<summary>Solution</summary>

```sql
ALTER VIEW EmployeeDirectory AS
SELECT ID, FullName
FROM Employee;
```

</details>

#### 9. After Question 8, what happens when you run `SELECT * FROM EmployeeDirectory`?

* A. It returns `ID`, `FullName`, and `Salary`.
* B. It returns only `ID` and `FullName`.
* C. It deletes data from `Employee`.
* D. It produces no rows.

<details>

<summary>Solution</summary>

**B. It returns only `ID` and `FullName`.**

`ALTER VIEW` updates the view definition.

</details>

#### 10. Remove the `HighSalaryEmployees` view. Does this remove rows from `Employee`?

<details>

<summary>Solution</summary>

```sql
DROP VIEW HighSalaryEmployees;
```

No. This removes only the saved view definition. The `Employee` data remains unchanged.

</details>

### Triggers

#### 11. Which event fires an `AFTER DELETE` trigger?

* A. A row is selected.
* B. A row is inserted.
* C. A row is updated.
* D. A row is deleted.

<details>

<summary>Solution</summary>

**D. A row is deleted.**

</details>

#### 12. Create `trg_AfterInsertEmployee`. Log each new employee in `Employee_Log` with the action `New Employee Added`.

<details>

<summary>Solution</summary>

```sql
CREATE TRIGGER trg_AfterInsertEmployee
ON Employee
AFTER INSERT
AS
BEGIN
    INSERT INTO Employee_Log (Action, EmployeeID)
    SELECT 'New Employee Added', ID
    FROM inserted;
END;
```

`inserted` contains the newly added rows.

</details>

#### 13. Test the trigger from Question 12 by adding employee `6`, `Neha Singh`, with salary `52000.00`. Then check the log.

<details>

<summary>Solution</summary>

```sql
INSERT INTO Employee (ID, FullName, Salary)
VALUES (6, 'Neha Singh', 52000.00);

SELECT *
FROM Employee_Log;
```

The log contains an entry for employee `6`.

</details>

#### 14. Fill in the blank. In an `AFTER INSERT` trigger, new rows are available in `__________`.

<details>

<summary>Solution</summary>

`inserted`

</details>

#### 15. Create `trg_AfterDeleteEmployee`. Log each deleted employee with the action `Employee Deleted`.

<details>

<summary>Solution</summary>

```sql
CREATE TRIGGER trg_AfterDeleteEmployee
ON Employee
AFTER DELETE
AS
BEGIN
    INSERT INTO Employee_Log (Action, EmployeeID)
    SELECT 'Employee Deleted', ID
    FROM deleted;
END;
```

`deleted` contains rows removed from `Employee`.

</details>

#### 16. Delete employee `6`, then display `Employee_Log` to verify the delete trigger.

<details>

<summary>Solution</summary>

```sql
DELETE FROM Employee
WHERE ID = 6;

SELECT *
FROM Employee_Log;
```

The log now includes `Employee Deleted` for employee `6`.

</details>

#### 17. During an `UPDATE` trigger, which special table holds the values before the update?

* A. `before`
* B. `old`
* C. `deleted`
* D. `inserted`

<details>

<summary>Solution</summary>

**C. `deleted`**

For an update, `deleted` holds old rows and `inserted` holds new rows.

</details>

#### 18. Create `trg_AfterUpdateEmployee`. Log each updated employee with the action `Employee Updated`.

<details>

<summary>Solution</summary>

```sql
CREATE TRIGGER trg_AfterUpdateEmployee
ON Employee
AFTER UPDATE
AS
BEGIN
    INSERT INTO Employee_Log (Action, EmployeeID)
    SELECT 'Employee Updated', ID
    FROM inserted;
END;
```

</details>

#### 19. Increase Amit Gupta's salary to `70000.00`. Then verify the update log.

<details>

<summary>Solution</summary>

```sql
UPDATE Employee
SET Salary = 70000.00
WHERE ID = 3;

SELECT *
FROM Employee_Log;
```

The trigger adds an `Employee Updated` entry for employee `3`.

</details>

#### 20. `inserted` contains rows only for an `INSERT` trigger. True or False?

<details>

<summary>Solution</summary>

**False.**

`inserted` is also available in an `UPDATE` trigger. It holds new values.

</details>

#### 21. Alter `trg_AfterInsertEmployee` so it logs `Employee Record Inserted` instead.

<details>

<summary>Solution</summary>

```sql
ALTER TRIGGER trg_AfterInsertEmployee
ON Employee
AFTER INSERT
AS
BEGIN
    INSERT INTO Employee_Log (Action, EmployeeID)
    SELECT 'Employee Record Inserted', ID
    FROM inserted;
END;
```

</details>

#### 22. Insert two employees in one statement: `6, 'Neha Singh', 52000.00` and `7, 'Karan Malhotra', 58000.00`. What should the insert trigger do?

<details>

<summary>Solution</summary>

```sql
INSERT INTO Employee (ID, FullName, Salary)
VALUES
(6, 'Neha Singh', 52000.00),
(7, 'Karan Malhotra', 58000.00);

SELECT *
FROM Employee_Log;
```

</details>

#### 23. Which statement removes a trigger named `trg_AfterUpdateEmployee`?

* A. `DELETE TRIGGER trg_AfterUpdateEmployee;`
* B. `DROP TRIGGER trg_AfterUpdateEmployee;`
* C. `REMOVE TRIGGER trg_AfterUpdateEmployee;`
* D. `TRUNCATE TRIGGER trg_AfterUpdateEmployee;`

<details>

<summary>Solution</summary>

**B. `DROP TRIGGER trg_AfterUpdateEmployee;`**

</details>

#### 24. Remove all three triggers created in this assignment. What happens to `Employee` and `Employee_Log`?

<details>

<summary>Solution</summary>

```sql
DROP TRIGGER trg_AfterInsertEmployee;
DROP TRIGGER trg_AfterDeleteEmployee;
DROP TRIGGER trg_AfterUpdateEmployee;
```

Only the triggers are removed. Both tables and their existing data remain available.

</details>
