---
description: >-
  Beginner-friendly practice questions on operators, DISTINCT, and sorting in
  SQL Server
---

# Practice Questions

### Use these questions to practice `WHERE`, operators, `DISTINCT`, and `ORDER BY` in SQL Server.

### Create sample tables

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2),
    City VARCHAR(50),
    JoinDate DATE
);

CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    City VARCHAR(50),
    State VARCHAR(50)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    TotalAmount DECIMAL(10,2),
    Status VARCHAR(30)
);

CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Category VARCHAR(50),
    Price DECIMAL(10,2),
    Stock INT
);

CREATE TABLE Branches (
    BranchID INT PRIMARY KEY,
    City VARCHAR(50),
    State VARCHAR(50)
);
```

#### Insert dummy data

```sql
INSERT INTO Employees (EmployeeID, EmployeeName, Department, Salary, City, JoinDate)
VALUES
(1, 'Aman Sharma', 'Sales', 52000, 'Delhi', '2022-03-15'),
(2, 'Priya Mehta', 'HR', 48000, 'Mumbai', '2023-01-10'),
(3, 'Rohan Verma', 'IT', 65000, 'Bengaluru', '2021-11-20'),
(4, 'Sneha Kapoor', 'Sales', 57000, 'Pune', '2022-07-05'),
(5, 'Arjun Nair', 'Finance', 72000, 'Chennai', '2024-02-18'),
(6, 'Anjali Rao', 'IT', 50000, 'Hyderabad', '2022-12-01');

INSERT INTO Customers (CustomerID, CustomerName, City, State)
VALUES
(101, 'Aditi Shah', 'Mumbai', 'Maharashtra'),
(102, 'Ankit Jain', 'Delhi', 'Delhi'),
(103, 'Meera Pillai', 'Chennai', 'Tamil Nadu'),
(104, 'Aman Khan', 'Pune', 'Maharashtra'),
(105, 'Riya Das', 'Kolkata', 'West Bengal'),
(106, 'Arun Patel', 'Ahmedabad', 'Gujarat');

INSERT INTO Orders (OrderID, CustomerID, OrderDate, TotalAmount, Status)
VALUES
(1001, 101, '2024-01-12', 2500.00, 'Delivered'),
(1002, 102, '2024-02-05', 1800.00, 'Pending'),
(1003, 103, '2024-03-18', 3200.00, 'Cancelled'),
(1004, 104, '2024-04-10', 1500.00, 'Delivered'),
(1005, 105, '2024-05-22', 4100.00, 'Shipped'),
(1006, 106, '2023-12-28', 900.00, 'Pending');

INSERT INTO Products (ProductID, ProductName, Category, Price, Stock)
VALUES
(201, 'Gel Pen', 'Stationery', 20.00, 100),
(202, 'Notebook', 'Stationery', 120.00, 200),
(203, 'Office Chair', 'Furniture', 3500.00, 15),
(204, 'Laptop Stand', 'Accessories', 1500.00, 40),
(205, 'Marker Pen', 'Stationery', 35.00, 80),
(206, 'Printer', 'Electronics', 8500.00, 10);

INSERT INTO Branches (BranchID, City, State)
VALUES
(1, 'Mumbai', 'Maharashtra'),
(2, 'Pune', 'Maharashtra'),
(3, 'Delhi', 'Delhi'),
(4, 'Chennai', 'Tamil Nadu'),
(5, 'Mumbai', 'Maharashtra'),
(6, 'Hyderabad', 'Telangana');
```

#### Check your data

```sql
SELECT * FROM Employees;
SELECT * FROM Customers;
SELECT * FROM Orders;
SELECT * FROM Products;
SELECT * FROM Branches;
```

Assume these tables exist:

* `Employees(EmployeeID, EmployeeName, Department, Salary, City, JoinDate)`
* `Customers(CustomerID, CustomerName, City, State)`
* `Orders(OrderID, CustomerID, OrderDate, TotalAmount, Status)`
* `Products(ProductID, ProductName, Category, Price, Stock)`
* `Branches(BranchID, City, State)`

### Operators Assignment:

#### 1. Write a query to show all employees who work in the `Sales` department.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Employees
WHERE Department = 'Sales';
```

</details>

#### 2. Write a query to show all products with a price greater than `1000`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Products
WHERE Price > 1000;
```

</details>

#### 3. Write a query to show all customers who do **not** live in `Mumbai`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Customers
WHERE City <> 'Mumbai';
```

`!=` also works in SQL Server.

</details>

#### 4. Write a query to show all employees whose salary is `50000` or more.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Employees
WHERE Salary >= 50000;
```

</details>

#### 5. Write a query to show all customers whose name starts with `A`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Customers
WHERE CustomerName LIKE 'A%';
```

</details>

#### 6. Write a query to show all products whose name ends with `Pen`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Products
WHERE ProductName LIKE '%Pen';
```

</details>

#### 7. Write a query to show all employees who joined before `2023-01-01`.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Employees
WHERE JoinDate < '2023-01-01';
```

</details>

#### 8. What is the difference between `=` and `LIKE` in SQL Server?

<details>

<summary>Solution</summary>

* `=` checks for an exact value.
* `LIKE` checks for a pattern.
* Example:
  * `City = 'Delhi'` finds only `Delhi`
  * `City LIKE 'D%'` finds any city that starts with `D`

</details>

### Distinct Assignment:

#### 1. Write a query to show all unique cities from the `Customers` table.

<details>

<summary>Solution</summary>

```sql
SELECT DISTINCT City
FROM Customers;
```

</details>

#### 2. Write a query to show all unique departments from the `Employees` table.

<details>

<summary>Solution</summary>

```sql
SELECT DISTINCT Department
FROM Employees;
```

</details>

#### 3. Write a query to show all unique order statuses from the `Orders` table.

<details>

<summary>Solution</summary>

```sql
SELECT DISTINCT Status
FROM Orders;
```

</details>

#### 4. What does `DISTINCT` do in SQL Server?

<details>

<summary>Solution</summary>

`DISTINCT` removes duplicate rows from the result and shows only unique values.

Example:

```sql
SELECT DISTINCT City
FROM Customers;
```

</details>

#### 5. Write a query to show unique combinations of `City` and `State` from the `Branches` table.

<details>

<summary>Solution</summary>

```sql
SELECT DISTINCT City, State
FROM Branches;
```

This returns unique pairs, not just unique cities.

</details>

### Sorting Assignment:&#x20;

#### 1. Write a query to show all products sorted by price from low to high.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Products
ORDER BY Price ASC;
```

</details>

#### 2. Write a query to show all employees sorted by salary from high to low.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Employees
ORDER BY Salary DESC;
```

</details>

#### 3. Write a query to show all customers sorted by `CustomerName` in alphabetical order.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Customers
ORDER BY CustomerName ASC;
```

</details>

#### 4. Write a query to show all orders from `2024-01-01` onward, sorted by newest order first.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Orders
WHERE OrderDate >= '2024-01-01'
ORDER BY OrderDate DESC;
```

</details>

#### 5. Write a query to show employees sorted by `Department` in ascending order and `Salary` in descending order.

<details>

<summary>Solution</summary>

```sql
SELECT *
FROM Employees
ORDER BY Department ASC, Salary DESC;
```

</details>

#### 6. What happens if you use `ORDER BY Price` without writing `ASC` or `DESC`?

<details>

<summary>Solution</summary>

SQL Server sorts the column in ascending order by default.

So this:

```sql
SELECT *
FROM Products
ORDER BY Price;
```

works the same as:

```sql
SELECT *
FROM Products
ORDER BY Price ASC;
```

</details>
