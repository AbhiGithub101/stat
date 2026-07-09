---
description: >-
  Beginner-friendly section-wise JOIN practice questions in SQL Server with
  sample data and solutions
hidden: true
---

# Practice Questions

### Sample data setup

> `Orders.CustomerID = 6` is intentional. It helps you practice unmatched rows.

#### Create sample tables

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    City VARCHAR(50)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    TotalAmount DECIMAL(10,2),
    OrderStatus VARCHAR(20)
);

CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(50)
);

CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    DepartmentID INT NULL,
    ManagerID INT NULL,
    Salary DECIMAL(10,2)
);

CREATE TABLE TShirtColors (
    ColorID INT PRIMARY KEY,
    ColorName VARCHAR(30)
);

CREATE TABLE TShirtSizes (
    SizeID INT PRIMARY KEY,
    SizeName VARCHAR(10)
);
```

#### Insert sample data

```sql
INSERT INTO Customers (CustomerID, CustomerName, City)
VALUES
(1, 'Aarav Mehta', 'Delhi'),
(2, 'Meera Nair', 'Mumbai'),
(3, 'Karan Shah', 'Pune'),
(4, 'Isha Verma', 'Chennai'),
(5, 'Rohan Das', 'Hyderabad');

INSERT INTO Orders (OrderID, CustomerID, OrderDate, TotalAmount, OrderStatus)
VALUES
(101, 1, '2024-06-01', 1200.00, 'Delivered'),
(102, 2, '2024-06-03', 850.00, 'Pending'),
(103, 2, '2024-06-07', 2200.00, 'Delivered'),
(104, 6, '2024-06-10', 1750.00, 'Cancelled'),
(105, 3, '2024-06-12', 950.00, 'Shipped');

INSERT INTO Departments (DepartmentID, DepartmentName)
VALUES
(10, 'Sales'),
(20, 'IT'),
(30, 'HR'),
(40, 'Finance');

INSERT INTO Employees (EmployeeID, EmployeeName, DepartmentID, ManagerID, Salary)
VALUES
(1, 'Neha Sharma', 20, NULL, 75000.00),
(2, 'Arjun Patel', 20, 1, 52000.00),
(3, 'Kavya Singh', 10, 4, 48000.00),
(4, 'Mohit Verma', 10, 1, 68000.00),
(5, 'Sana Khan', 30, NULL, 62000.00),
(6, 'Riya Das', 40, 5, 45000.00);

INSERT INTO TShirtColors (ColorID, ColorName)
VALUES
(1, 'Red'),
(2, 'Blue'),
(3, 'Black');

INSERT INTO TShirtSizes (SizeID, SizeName)
VALUES
(1, 'S'),
(2, 'M'),
(3, 'L');
```

#### Check the data

```sql
SELECT * FROM Customers;
SELECT * FROM Orders;
SELECT * FROM Departments;
SELECT * FROM Employees;
SELECT * FROM TShirtColors;
SELECT * FROM TShirtSizes;
```

### INNER JOIN questions

Use these tables:

* `Customers(CustomerID, CustomerName, City)`
* `Orders(OrderID, CustomerID, OrderDate, TotalAmount, OrderStatus)`

#### 1. Write a query to show customer names and their order IDs.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, O.OrderID
FROM Customers AS C
INNER JOIN Orders AS O
    ON C.CustomerID = O.CustomerID;
```

</details>

#### 2. Write a query to show order ID, customer name, and total amount.

<details>

<summary>Solution</summary>

```sql
SELECT O.OrderID, C.CustomerName, O.TotalAmount
FROM Customers AS C
INNER JOIN Orders AS O
    ON C.CustomerID = O.CustomerID;
```

</details>

#### 3. Write a query to show only delivered orders with customer names.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, O.OrderID, O.OrderStatus
FROM Customers AS C
INNER JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
WHERE O.OrderStatus = 'Delivered';
```

</details>

#### 4. Write a query to show customers from `Mumbai` or `Delhi` who placed orders.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, C.City, O.OrderID
FROM Customers AS C
INNER JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
WHERE C.City IN ('Mumbai', 'Delhi');
```

</details>

#### 5. Write a query to count how many matched customer orders exist.

<details>

<summary>Solution</summary>

```sql
SELECT COUNT(*) AS MatchedOrders
FROM Customers AS C
INNER JOIN Orders AS O
    ON C.CustomerID = O.CustomerID;
```

</details>

### LEFT JOIN questions

#### 1. Write a query to show all customers and their order IDs.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, O.OrderID
FROM Customers AS C
LEFT JOIN Orders AS O
    ON C.CustomerID = O.CustomerID;
```

</details>

#### 2. Write a query to find customers who have no orders.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerID, C.CustomerName
FROM Customers AS C
LEFT JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
WHERE O.OrderID IS NULL;
```

</details>

#### 3. Write a query to count the number of orders for each customer, including customers with zero orders.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, COUNT(O.OrderID) AS TotalOrders
FROM Customers AS C
LEFT JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
GROUP BY C.CustomerName;
```

</details>

#### 4. Write a query to show all customers and only their delivered orders.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, O.OrderID, O.OrderStatus
FROM Customers AS C
LEFT JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
   AND O.OrderStatus = 'Delivered';
```

This keeps all customers.

Only delivered orders appear from the `Orders` table.

</details>

### RIGHT JOIN questions

#### 1. Write a query to show all orders and matching customer names.

<details>

<summary>Solution</summary>

```sql
SELECT O.OrderID, C.CustomerName, O.OrderStatus
FROM Customers AS C
RIGHT JOIN Orders AS O
    ON C.CustomerID = O.CustomerID;
```

</details>

#### 2. Write a query to find orders that do not have a matching customer.

<details>

<summary>Solution</summary>

```sql
SELECT O.OrderID, O.CustomerID, O.OrderStatus
FROM Customers AS C
RIGHT JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
WHERE C.CustomerID IS NULL;
```

</details>

#### 3. Write a query to show all orders with customer names and sort by order ID.

<details>

<summary>Solution</summary>

```sql
SELECT O.OrderID, C.CustomerName, O.TotalAmount
FROM Customers AS C
RIGHT JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
ORDER BY O.OrderID;
```

</details>

### FULL OUTER JOIN questions

#### 1. Write a query to show all customers and all orders.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, O.OrderID, O.OrderStatus
FROM Customers AS C
FULL OUTER JOIN Orders AS O
    ON C.CustomerID = O.CustomerID;
```

</details>

#### 2. Write a query to show only unmatched rows from both tables.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, O.OrderID, O.CustomerID
FROM Customers AS C
FULL OUTER JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
WHERE C.CustomerID IS NULL
   OR O.OrderID IS NULL;
```

</details>

### SELF JOIN questions

Use these tables:

* `Employees(EmployeeID, EmployeeName, DepartmentID, ManagerID, Salary)`
* `Departments(DepartmentID, DepartmentName)`

#### 1. Write a query to show each employee and their manager name.

<details>

<summary>Solution</summary>

```sql
SELECT E.EmployeeName AS Employee,
       M.EmployeeName AS Manager
FROM Employees AS E
LEFT JOIN Employees AS M
    ON E.ManagerID = M.EmployeeID;
```

</details>

#### 2. Write a query to show employees who do not have a manager.

<details>

<summary>Solution</summary>

```sql
SELECT EmployeeID, EmployeeName
FROM Employees
WHERE ManagerID IS NULL;
```

</details>

#### 3. Write a query to show employees managed by `Neha Sharma`.

<details>

<summary>Solution</summary>

```sql
SELECT E.EmployeeName
FROM Employees AS E
INNER JOIN Employees AS M
    ON E.ManagerID = M.EmployeeID
WHERE M.EmployeeName = 'Neha Sharma';
```

</details>

### CROSS JOIN questions

Use these tables:

* `TShirtColors(ColorID, ColorName)`
* `TShirtSizes(SizeID, SizeName)`

#### 1. Write a query to show all possible T-shirt color and size combinations.

<details>

<summary>Solution</summary>

```sql
SELECT C.ColorName, S.SizeName
FROM TShirtColors AS C
CROSS JOIN TShirtSizes AS S;
```

</details>

#### 2. Write a query to count the total number of possible combinations.

<details>

<summary>Solution</summary>

```sql
SELECT COUNT(*) AS TotalCombinations
FROM TShirtColors AS C
CROSS JOIN TShirtSizes AS S;
```

</details>

#### 3. Write a query to show all combinations, sorted by color and then size.

<details>

<summary>Solution</summary>

```sql
SELECT C.ColorName, S.SizeName
FROM TShirtColors AS C
CROSS JOIN TShirtSizes AS S
ORDER BY C.ColorName, S.SizeName;
```

</details>

### Intermediate mixed join questions

#### 1. Write a query to show customer name, order ID, and order date for all matched records. Sort by newest order first.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, O.OrderID, O.OrderDate
FROM Customers AS C
INNER JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
ORDER BY O.OrderDate DESC;
```

</details>

#### 2. Write a query to show all customers and their order status. Include customers who have no orders.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, O.OrderStatus
FROM Customers AS C
LEFT JOIN Orders AS O
    ON C.CustomerID = O.CustomerID;
```

</details>

#### 3. Write a query to show all orders where the customer name is missing.

<details>

<summary>Solution</summary>

```sql
SELECT O.OrderID, O.CustomerID, O.TotalAmount
FROM Customers AS C
RIGHT JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
WHERE C.CustomerName IS NULL;
```

</details>

#### 4. Write a query to show customer names and order amounts for orders greater than `1000`.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, O.TotalAmount
FROM Customers AS C
INNER JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
WHERE O.TotalAmount > 1000;
```

</details>

#### 5. Write a query to show all customers and their latest possible order details, but only for orders placed on or after `2024-06-05`.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, O.OrderID, O.OrderDate
FROM Customers AS C
LEFT JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
   AND O.OrderDate >= '2024-06-05';
```

</details>

#### 6. Write a query to show employee names and department names for employees who belong to a department.

<details>

<summary>Solution</summary>

```sql
SELECT E.EmployeeName, D.DepartmentName
FROM Employees AS E
INNER JOIN Departments AS D
    ON E.DepartmentID = D.DepartmentID;
```

</details>

#### 7. Write a query to show all employees and their department names. Include employees even if no department is assigned.

<details>

<summary>Solution</summary>

```sql
SELECT E.EmployeeName, D.DepartmentName
FROM Employees AS E
LEFT JOIN Departments AS D
    ON E.DepartmentID = D.DepartmentID;
```

</details>

#### 8. Write a query to show departments that currently have no employees.

<details>

<summary>Solution</summary>

```sql
SELECT D.DepartmentID, D.DepartmentName
FROM Employees AS E
RIGHT JOIN Departments AS D
    ON E.DepartmentID = D.DepartmentID
WHERE E.EmployeeID IS NULL;
```

</details>

#### 9. Write a query to show all employees and all departments, including unmatched rows from both sides.

<details>

<summary>Solution</summary>

```sql
SELECT E.EmployeeName, D.DepartmentName
FROM Employees AS E
FULL OUTER JOIN Departments AS D
    ON E.DepartmentID = D.DepartmentID;
```

</details>

#### 10. Write a query to show only unmatched rows between `Employees` and `Departments`.

<details>

<summary>Solution</summary>

```sql
SELECT E.EmployeeName, D.DepartmentName
FROM Employees AS E
FULL OUTER JOIN Departments AS D
    ON E.DepartmentID = D.DepartmentID
WHERE E.EmployeeID IS NULL
   OR D.DepartmentID IS NULL;
```

</details>

#### 11. Write a query to show each employee and their manager, but exclude employees who do not have a manager.

<details>

<summary>Solution</summary>

```sql
SELECT E.EmployeeName AS Employee,
       M.EmployeeName AS Manager
FROM Employees AS E
INNER JOIN Employees AS M
    ON E.ManagerID = M.EmployeeID;
```

</details>

#### 12. Write a query to show employees whose manager name starts with `N`.

<details>

<summary>Solution</summary>

```sql
SELECT E.EmployeeName AS Employee,
       M.EmployeeName AS Manager
FROM Employees AS E
INNER JOIN Employees AS M
    ON E.ManagerID = M.EmployeeID
WHERE M.EmployeeName LIKE 'N%';
```

</details>

#### 13. Write a query to show all possible color and size combinations, but only for size `M`.

<details>

<summary>Solution</summary>

```sql
SELECT C.ColorName, S.SizeName
FROM TShirtColors AS C
CROSS JOIN TShirtSizes AS S
WHERE S.SizeName = 'M';
```

</details>

#### 14. Write a query to show all possible combinations where the color is not `Black`.

<details>

<summary>Solution</summary>

```sql
SELECT C.ColorName, S.SizeName
FROM TShirtColors AS C
CROSS JOIN TShirtSizes AS S
WHERE C.ColorName <> 'Black';
```

</details>

#### 15. Write a query to show customer name and order amount for matched records. Replace a missing customer name with `Unknown Customer`.

<details>

<summary>Solution</summary>

```sql
SELECT ISNULL(C.CustomerName, 'Unknown Customer') AS CustomerName,
       O.TotalAmount
FROM Customers AS C
RIGHT JOIN Orders AS O
    ON C.CustomerID = O.CustomerID;
```

</details>

### Challenging and interesting questions

#### 1. Write a query to show customers who placed more than one order.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, COUNT(O.OrderID) AS TotalOrders
FROM Customers AS C
INNER JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
GROUP BY C.CustomerName
HAVING COUNT(O.OrderID) > 1;
```

</details>

#### 2. Write a query to show customers with no orders and orders with no customers in one result.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, O.OrderID, O.CustomerID
FROM Customers AS C
FULL OUTER JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
WHERE C.CustomerID IS NULL
   OR O.OrderID IS NULL;
```

</details>

#### 3. Write a query to show each manager and the number of employees reporting to them.

<details>

<summary>Solution</summary>

```sql
SELECT M.EmployeeName AS Manager,
       COUNT(E.EmployeeID) AS TeamMembers
FROM Employees AS M
LEFT JOIN Employees AS E
    ON E.ManagerID = M.EmployeeID
GROUP BY M.EmployeeName
HAVING COUNT(E.EmployeeID) > 0;
```

</details>

#### 5. Write a query to show employee name, manager name, department name, and salary. Sort by salary from high to low.

<details>

<summary>Solution</summary>

```sql
SELECT E.EmployeeName,
       M.EmployeeName AS ManagerName,
       D.DepartmentName,
       E.Salary
FROM Employees AS E
LEFT JOIN Employees AS M
    ON E.ManagerID = M.EmployeeID
LEFT JOIN Departments AS D
    ON E.DepartmentID = D.DepartmentID
ORDER BY E.Salary DESC;
```

</details>

#### 6. Write a query to show all T-shirt combinations for only `Red` and `Blue` colors.

<details>

<summary>Solution</summary>

```sql
SELECT C.ColorName, S.SizeName
FROM TShirtColors AS C
CROSS JOIN TShirtSizes AS S
WHERE C.ColorName IN ('Red', 'Blue')
ORDER BY C.ColorName, S.SizeName;
```

</details>

#### 7. Write a query to show each customer and the number of delivered orders they placed. Include customers with zero delivered orders.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName,
       COUNT(O.OrderID) AS DeliveredOrders
FROM Customers AS C
LEFT JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
   AND O.OrderStatus = 'Delivered'
GROUP BY C.CustomerName;
```

</details>

#### 8. Write a query to show only the matched customer orders with amount greater than `1000`.

<details>

<summary>Solution</summary>

```sql
SELECT C.CustomerName, O.OrderID, O.TotalAmount
FROM Customers AS C
INNER JOIN Orders AS O
    ON C.CustomerID = O.CustomerID
WHERE O.TotalAmount > 1000;
```

</details>
