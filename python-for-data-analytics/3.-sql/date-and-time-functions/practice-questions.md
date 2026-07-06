---
description: Beginner-friendly practice questions on date and time functions in SQL Server
---

# Practice Questions

### Create sample tables

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Department VARCHAR(50),
    BirthDate DATE,
    JoinDate DATE,
    ShiftStart DATETIME,
    ShiftEnd DATETIME
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    OrderDate DATETIME,
    DispatchDate DATETIME,
    DeliveryDate DATE,
    Amount DECIMAL(10,2)
);

CREATE TABLE Subscriptions (
    SubscriptionID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    StartDate DATE,
    RenewalDate DATE,
    ExpiryDate DATE,
    PlanName VARCHAR(50)
);
```

### Insert sample data

```sql
INSERT INTO Employees (EmployeeID, EmployeeName, Department, BirthDate, JoinDate, ShiftStart, ShiftEnd)
VALUES
(1, 'Aman Sharma', 'Sales', '1998-04-12', '2023-01-15', '2026-07-01 09:00:00', '2026-07-01 18:00:00'),
(2, 'Priya Mehta', 'HR', '1996-09-25', '2022-06-20', '2026-07-01 10:00:00', '2026-07-01 19:00:00'),
(3, 'Rohan Verma', 'IT', '2000-02-18', '2024-03-10', '2026-07-02 08:30:00', '2026-07-02 17:30:00'),
(4, 'Sneha Kapoor', 'Finance', '1997-12-05', '2021-11-01', '2026-07-02 09:30:00', '2026-07-02 18:30:00'),
(5, 'Neha Joshi', 'Support', '1999-07-08', '2025-02-05', '2026-07-03 11:00:00', '2026-07-03 20:00:00');

INSERT INTO Orders (OrderID, CustomerName, OrderDate, DispatchDate, DeliveryDate, Amount)
VALUES
(101, 'Riya Shah', '2026-06-01 10:15:00', '2026-06-02 14:00:00', '2026-06-05', 2500.00),
(102, 'Arjun Nair', '2026-06-10 16:45:00', '2026-06-11 11:30:00', '2026-06-14', 4200.00),
(103, 'Meera Iyer', '2026-06-15 09:20:00', '2026-06-16 15:10:00', '2026-06-18', 1800.00),
(104, 'Karan Patel', '2026-06-20 18:05:00', '2026-06-21 10:45:00', '2026-06-25', 3100.00),
(105, 'Sara Khan', '2026-06-28 12:00:00', '2026-06-29 13:15:00', '2026-07-02', 2750.00);

INSERT INTO Subscriptions (SubscriptionID, CustomerName, StartDate, RenewalDate, ExpiryDate, PlanName)
VALUES
(201, 'Ankit Jain', '2026-01-01', '2026-07-01', '2026-12-31', 'Gold'),
(202, 'Pooja Singh', '2026-02-15', '2026-08-15', '2027-02-14', 'Silver'),
(203, 'Rahul Das', '2026-03-10', '2026-09-10', '2027-03-09', 'Gold'),
(204, 'Isha Kapoor', '2026-04-05', '2026-10-05', '2027-04-04', 'Basic'),
(205, 'Vikram Rao', '2026-05-20', '2026-11-20', '2027-05-19', 'Premium');
```

### Check your data

```sql
SELECT * FROM Employees;
SELECT * FROM Orders;
SELECT * FROM Subscriptions;
```

Assume these tables exist:

* `Employees(EmployeeID, EmployeeName, Department, BirthDate, JoinDate, ShiftStart, ShiftEnd)`
* `Orders(OrderID, CustomerName, OrderDate, DispatchDate, DeliveryDate, Amount)`
* `Subscriptions(SubscriptionID, CustomerName, StartDate, RenewalDate, ExpiryDate, PlanName)`

### Questions:

#### 1. Write a query to show the current date and time.

<details>

<summary>Solution</summary>

```sql
SELECT GETDATE() AS CurrentDateTime;
```

</details>

#### 2. Write a query to show the current UTC date and time.

<details>

<summary>Solution</summary>

```sql
SELECT GETUTCDATE() AS UTCDateTime;
```

</details>

#### 3. Write a query to show each employee name and joining year.

<details>

<summary>Solution</summary>

```sql
SELECT EmployeeName,
       YEAR(JoinDate) AS JoiningYear
FROM Employees;
```

</details>

#### 4. Write a query to show each order ID and order month.

<details>

<summary>Solution</summary>

```sql
SELECT OrderID,
       MONTH(OrderDate) AS OrderMonth
FROM Orders;
```

</details>

#### 5. Write a query to show each employee name and birth day of the month.

<details>

<summary>Solution</summary>

```sql
SELECT EmployeeName,
       DAY(BirthDate) AS BirthDay
FROM Employees;
```

</details>

#### 6. Write a query to show the hour part from `ShiftStart` for each employee.

<details>

<summary>Solution</summary>

```sql
SELECT EmployeeName,
       DATEPART(hour, ShiftStart) AS ShiftStartHour
FROM Employees;
```

</details>

#### 7. Write a query to show the quarter of each subscription start date.

<details>

<summary>Solution</summary>

```sql
SELECT SubscriptionID,
       DATEPART(quarter, StartDate) AS StartQuarter
FROM Subscriptions;
```

</details>

#### 8. Write a query to show each employee name and the weekday of their join date.

<details>

<summary>Solution</summary>

```sql
SELECT EmployeeName,
       DATENAME(weekday, JoinDate) AS JoinDayName
FROM Employees;
```

</details>

#### 9. Write a query to show each order ID and the month name of the order date.

<details>

<summary>Solution</summary>

```sql
SELECT OrderID,
       DATENAME(month, OrderDate) AS OrderMonthName
FROM Orders;
```

</details>

#### 10. Write a query to show the last date of the month for each order date.

<details>

<summary>Solution</summary>

```sql
SELECT OrderID,
       OrderDate,
       EOMONTH(OrderDate) AS MonthEndDate
FROM Orders;
```

</details>

#### 11. Write a query to show each subscription renewal date after adding 30 days.

<details>

<summary>Solution</summary>

```sql
SELECT SubscriptionID,
       RenewalDate,
       DATEADD(day, 30, RenewalDate) AS RenewalPlus30Days
FROM Subscriptions;
```

</details>

#### 12. Write a query to show each employee join date after adding 1 year.

<details>

<summary>Solution</summary>

```sql
SELECT EmployeeName,
       JoinDate,
       DATEADD(year, 1, JoinDate) AS JoinDateAfter1Year
FROM Employees;
```

</details>

#### 13. Write a query to show each order date 2 days before the actual order date.

<details>

<summary>Solution</summary>

```sql
SELECT OrderID,
       OrderDate,
       DATEADD(day, -2, OrderDate) AS TwoDaysBeforeOrder
FROM Orders;
```

</details>

#### 14. Write a query to show each shift end time after adding 2 hours.

<details>

<summary>Solution</summary>

```sql
SELECT EmployeeName,
       ShiftEnd,
       DATEADD(hour, 2, ShiftEnd) AS ShiftEndPlus2Hours
FROM Employees;
```

</details>

#### 15. Write a query to show how many days each order took to deliver.

<details>

<summary>Solution</summary>

```sql
SELECT OrderID,
       DATEDIFF(day, OrderDate, DeliveryDate) AS DeliveryDays
FROM Orders;
```

</details>

#### 16. Write a query to show how many months are there between subscription start date and expiry date.

<details>

<summary>Solution</summary>

```sql
SELECT SubscriptionID,
       DATEDIFF(month, StartDate, ExpiryDate) AS TotalMonths
FROM Subscriptions;
```

</details>

#### 17. Write a query to show how many years have passed since each employee joined.

<details>

<summary>Solution</summary>

```sql
SELECT EmployeeName,
       DATEDIFF(year, JoinDate, GETDATE()) AS YearsSinceJoining
FROM Employees;
```

</details>

#### 18. Write a query to show the number of hours between `ShiftStart` and `ShiftEnd`.

<details>

<summary>Solution</summary>

```sql
SELECT EmployeeName,
       DATEDIFF(hour, ShiftStart, ShiftEnd) AS ShiftHours
FROM Employees;
```

</details>

#### 19. Convert the text `'2026-07-15'` into a `DATE` using `CAST()`.

<details>

<summary>Solution</summary>

```sql
SELECT CAST('2026-07-15' AS DATE) AS ConvertedDate;
```

</details>

#### 20. Convert the text `'2026-07-15 14:45:00'` into a `DATETIME` using `CONVERT()`.

<details>

<summary>Solution</summary>

```sql
SELECT CONVERT(DATETIME, '2026-07-15 14:45:00') AS ConvertedDateTime;
```

</details>

#### 21. Which function can convert one data type to another: `CAST()` or `CONVERT()`?

<details>

<summary>Solution</summary>

Both `CAST()` and `CONVERT()` can convert one data type to another.

</details>

### Formatting dates with `CONVERT()` styles

#### 22. Write a query to show the current date in `DD/MM/YYYY` format.

<details>

<summary>Solution</summary>

```sql
SELECT CONVERT(VARCHAR, GETDATE(), 103) AS IndianDateFormat;
```

</details>

#### 23. Write a query to show the current date in `MM/DD/YYYY` format.

<details>

<summary>Solution</summary>

```sql
SELECT CONVERT(VARCHAR, GETDATE(), 101) AS USDateFormat;
```

</details>

#### 24. Write a query to show each order date in `YYYYMMDD` format.

<details>

<summary>Solution</summary>

```sql
SELECT OrderID,
       CONVERT(VARCHAR, OrderDate, 112) AS CompactOrderDate
FROM Orders;
```

</details>

#### 25. Write a query to show each delivery date in `DD Mon YYYY` format.

<details>

<summary>Solution</summary>

```sql
SELECT OrderID,
       CONVERT(VARCHAR, DeliveryDate, 106) AS DeliveryDateFormatted
FROM Orders;
```

</details>

#### 26. Write a query to show each employee name, join year, and join month name.

<details>

<summary>Solution</summary>

```sql
SELECT EmployeeName,
       YEAR(JoinDate) AS JoinYear,
       DATENAME(month, JoinDate) AS JoinMonthName
FROM Employees;
```

</details>

#### 27. Write a query to show each subscription ID and the last date of its renewal month.

<details>

<summary>Solution</summary>

```sql
SELECT SubscriptionID,
       RenewalDate,
       EOMONTH(RenewalDate) AS RenewalMonthEnd
FROM Subscriptions;
```

</details>

#### 28. Write a query to show each order ID, order month name, and end of that month.

<details>

<summary>Solution</summary>

```sql
SELECT OrderID,
       DATENAME(month, OrderDate) AS OrderMonthName,
       EOMONTH(OrderDate) AS OrderMonthEnd
FROM Orders;
```

</details>
