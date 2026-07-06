# Practice Questions

### Reference tables for practice

Use these sample tables where needed:

```sql
CREATE TABLE Employees (
    EmployeeID INT IDENTITY(1,1) PRIMARY KEY,
    FullName VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2),
    HireDate DATE
);

CREATE TABLE Customers (
    CustomerID INT IDENTITY(1,1) PRIMARY KEY,
    CustomerName VARCHAR(100),
    City VARCHAR(50)
);

CREATE TABLE Orders (
    OrderID INT IDENTITY(1001,1) PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    TotalAmount DECIMAL(10,2)
);
```



#### 1. What is the difference between DDL and DML?

<details>

<summary>Solution</summary>

* **DDL** changes the table structure.
* Examples: `CREATE`, `ALTER`, `DROP`, `TRUNCATE`
* **DML** changes the data inside the table.
* Examples: `INSERT`, `UPDATE`, `DELETE`

</details>

#### 2. Write a query to create a table named `Departments` with these columns:

* `DepartmentID` as primary key
* `DepartmentName` as `VARCHAR(50)`
* `Location` as `VARCHAR(50)`

<details>

<summary>Solution</summary>

```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(50),
    Location VARCHAR(50)
);
```

</details>

#### 3. Write a query to add a new column named `PhoneNumber` to the `Customers` table.

<details>

<summary>Solution</summary>

```sql
ALTER TABLE Customers
ADD PhoneNumber VARCHAR(20);
```

</details>

#### 4. Write a query to increase the size of `CustomerName` in the `Customers` table from `VARCHAR(100)` to `VARCHAR(150)`.

<details>

<summary>Solution</summary>

```sql
ALTER TABLE Customers
ALTER COLUMN CustomerName VARCHAR(150);
```

</details>

#### 5. Write a query to remove the `Location` column from the `Departments` table.

<details>

<summary>Solution</summary>

```sql
ALTER TABLE Departments
DROP COLUMN Location;
```

</details>

#### 6. What does `IDENTITY(1,1)` mean in SQL Server?

<details>

<summary>Solution</summary>

`IDENTITY(1,1)` means:

* Start from `1`
* Increase by `1` for every new row

Example generated values:

```sql
1, 2, 3, 4, 5 ...
```

</details>

#### 7. Write a query to insert a new employee named `Rohan Mehta` into `Employees`.

Use:

* Department: `Sales`
* Salary: `45000`
* HireDate: `2024-01-15`

<details>

<summary>Solution</summary>

```sql
INSERT INTO Employees (FullName, Department, Salary, HireDate)
VALUES ('Rohan Mehta', 'Sales', 45000, '2024-01-15');
```

</details>

#### 8. Write a query to update the salary of the employee whose `EmployeeID` is `3` to `52000`.

<details>

<summary>Solution</summary>

```sql
UPDATE Employees
SET Salary = 52000
WHERE EmployeeID = 3;
```

</details>

#### 9. Why is the `WHERE` clause important in an `UPDATE` query?

<details>

<summary>Solution</summary>

`WHERE` tells SQL Server which row to update.

Without `WHERE`, all rows are updated.

Example:

```sql
UPDATE Employees
SET Department = 'HR';
```

This changes the department for every employee.

</details>

#### 10. Write a query to change the department of all employees in `Sales` to `Marketing`.

<details>

<summary>Solution</summary>

```sql
UPDATE Employees
SET Department = 'Marketing'
WHERE Department = 'Sales';
```

</details>

#### 11. Write a query to delete the customer whose `CustomerID` is `4`.

<details>

<summary>Solution</summary>

```sql
DELETE FROM Customers
WHERE CustomerID = 4;
```

</details>

#### 12. What happens if you run `DELETE FROM Customers;` without a `WHERE` clause?

<details>

<summary>Solution</summary>

All rows are deleted from the `Customers` table.

The table still exists.

Only the data is removed.

</details>

#### 13. Write a query to delete all orders where `TotalAmount` is less than `500`.

<details>

<summary>Solution</summary>

```sql
DELETE FROM Orders
WHERE TotalAmount < 500;
```

</details>

#### 14. Write a query to insert a new customer named `Anita Rao` from `Pune`.

<details>

<summary>Solution</summary>

```sql
INSERT INTO Customers (CustomerName, City)
VALUES ('Anita Rao', 'Pune');
```

</details>

#### 15. Write a query to update both the `CustomerName` and `City` for `CustomerID = 2`.

Change:

* `CustomerName` to `Vikram Shah`
* `City` to `Ahmedabad`

<details>

<summary>Solution</summary>

```sql
UPDATE Customers
SET CustomerName = 'Vikram Shah',
    City = 'Ahmedabad'
WHERE CustomerID = 2;
```

</details>

#### 19. A new order should start from `5001` and increase by `1`.

How would you define the `OrderID` column?

<details>

<summary>Solution</summary>

```sql
OrderID INT IDENTITY(5001,1) PRIMARY KEY
```

</details>

#### 20. Write a query to find all employees who work in `IT`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Employees
WHERE Department = 'IT';
```

</details>
