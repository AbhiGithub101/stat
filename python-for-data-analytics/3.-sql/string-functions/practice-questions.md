---
description: practice questions on string functions with sample data and answers
---

# Practice Questions

### Create sample tables

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FullName NVARCHAR(100),
    City VARCHAR(50),
    Email VARCHAR(100),
    CustomerCode VARCHAR(20)
);

CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName NVARCHAR(100),
    Department VARCHAR(50),
    WorkEmail VARCHAR(100),
    BranchCode VARCHAR(20)
);
```

### Insert sample data

```sql
INSERT INTO Customers (CustomerID, FullName, City, Email, CustomerCode)
VALUES
(1, '  Aditi Sharma  ', 'Mumbai', 'aditi.sharma@gmail.com', 'CUST-101-MUM'),
(2, 'Rohan Mehta', 'Delhi', 'rohan.mehta@gmail.com', 'CUST-102-DEL'),
(3, 'Sneha Iyer', 'Chennai', 'sneha.iyer@gmail.com', 'CUST-103-CHE'),
(4, ' Arjun Nair', 'Bengaluru', 'arjun.nair@gmail.com', 'CUST-104-BLR'),
(5, 'Meera Joshi   ', 'Pune', 'meera.joshi@gmail.com', 'CUST-105-PUN');

INSERT INTO Employees (EmployeeID, EmployeeName, Department, WorkEmail, BranchCode)
VALUES
(101, 'Priya Verma', 'Sales', 'priya.verma@company.com', 'DEL-EMP-01'),
(102, '  Amit Kumar', 'HR', 'amit.kumar@company.com', 'MUM-EMP-02'),
(103, 'Neha Kapoor  ', 'IT', 'neha.kapoor@company.com', 'CHE-EMP-03'),
(104, 'Vikas Rao', 'Finance', 'vikas.rao@company.com', 'HYD-EMP-04'),
(105, 'Sara Khan', 'Support', 'sara.khan@company.com', 'PUN-EMP-05');
```

### Check your data

```sql
SELECT * FROM Customers;
SELECT * FROM Employees;
```

Assume these tables exist:

* `Customers(CustomerID, FullName, City, Email, CustomerCode)`
* `Employees(EmployeeID, EmployeeName, Department, WorkEmail, BranchCode)`

## Questions:

#### 1. Write a query to show each customer name with its character count.

<details>

<summary>Solution</summary>

```sql
SELECT FullName, LEN(FullName) AS NameLength
FROM Customers;
```

</details>

#### 2. Write a query to show each employee name with both `LEN()` and `DATALENGTH()`.

<details>

<summary>Solution</summary>

```sql
SELECT EmployeeName,
       LEN(EmployeeName) AS CharacterCount,
       DATALENGTH(EmployeeName) AS ByteCount
FROM Employees;
```

</details>

#### 3. Which function counts bytes instead of characters?

<details>

<summary>Solution</summary>

`DATALENGTH()` counts bytes.

`LEN()` counts characters.

</details>

#### 4. Write a query to show all customer names in uppercase.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       UPPER(FullName) AS UpperName
FROM Customers;
```

</details>

#### 5. Write a query to show all employee department names in lowercase.

<details>

<summary>Solution</summary>

```sql
SELECT Department,
       LOWER(Department) AS LowerDepartment
FROM Employees;
```

</details>

#### 6. Write a query to show customer city names in uppercase.

<details>

<summary>Solution</summary>

```sql
SELECT City,
       UPPER(City) AS UpperCity
FROM Customers;
```

</details>

#### 7. Write a query to remove spaces from both sides of `FullName`.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       TRIM(FullName) AS CleanName
FROM Customers;
```

</details>

#### 8. Write a query to remove spaces only from the left side of `EmployeeName`.

<details>

<summary>Solution</summary>

```sql
SELECT EmployeeName,
       LTRIM(EmployeeName) AS LeftCleanedName
FROM Employees;
```

</details>

#### 9. Write a query to remove spaces only from the right side of `FullName`.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       RTRIM(FullName) AS RightCleanedName
FROM Customers;
```

</details>

#### 10. Write a query to show the first 5 characters of each customer name after removing extra spaces.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       SUBSTRING(TRIM(FullName), 1, 5) AS FirstFiveChars
FROM Customers;
```

</details>

#### 11. Write a query to extract `101` from the value `CUST-101-MUM`.

<details>

<summary>Solution</summary>

```sql
SELECT SUBSTRING('CUST-101-MUM', 6, 3) AS CodePart;
```

</details>

#### 12. Write a query to show the first 4 characters of every branch code.

<details>

<summary>Solution</summary>

```sql
SELECT BranchCode,
       SUBSTRING(BranchCode, 1, 4) AS FirstPart
FROM Employees;
```

</details>

#### 13. Write a query to show the first 3 characters of each city name.

<details>

<summary>Solution</summary>

```sql
SELECT City,
       LEFT(City, 3) AS CityShortName
FROM Customers;
```

</details>

#### 14. Write a query to show the last 3 characters of each customer code.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCode,
       RIGHT(CustomerCode, 3) AS CityCode
FROM Customers;
```

</details>

#### 15. Write a query to show the first 3 letters of each employee department.

<details>

<summary>Solution</summary>

```sql
SELECT Department,
       LEFT(Department, 3) AS DeptShortName
FROM Employees;
```

</details>

#### 16. Write a query to show the last 2 characters of each branch code.

<details>

<summary>Solution</summary>

```sql
SELECT BranchCode,
       RIGHT(BranchCode, 2) AS BranchNumber
FROM Employees;
```

</details>

#### 17. Write a query to find the position of `@` in each employee email.

<details>

<summary>Solution</summary>

```sql
SELECT WorkEmail,
       CHARINDEX('@', WorkEmail) AS AtPosition
FROM Employees;
```

</details>

#### 18. Write a query to reverse each customer city name.

<details>

<summary>Solution</summary>

```sql
SELECT City,
       REVERSE(City) AS ReversedCity
FROM Customers;
```

</details>

#### 19. What does `CHARINDEX()` return when the searched text is not found?

<details>

<summary>Solution</summary>

`CHARINDEX()` returns `0`.

</details>

#### 20. Write a query to replace `company.com` with `office.com` in employee emails.

<details>

<summary>Solution</summary>

```sql
SELECT WorkEmail,
       REPLACE(WorkEmail, 'company.com', 'office.com') AS UpdatedEmail
FROM Employees;
```

</details>

#### 21. Write a query to replace `CUST` with `CUS` in each customer code.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCode,
       REPLACE(CustomerCode, 'CUST', 'CUS') AS NewCustomerCode
FROM Customers;
```

</details>

#### 22. Write a query to combine customer name and city in one column using `-` between them.

<details>

<summary>Solution</summary>

```sql
SELECT CONCAT(TRIM(FullName), ' - ', City) AS CustomerDetails
FROM Customers;
```

</details>

#### 23. Write a query to combine employee name and department in one column using `works in` between them.

<details>

<summary>Solution</summary>

```sql
SELECT CONCAT(TRIM(EmployeeName), ' works in ', Department) AS EmployeeInfo
FROM Employees;
```

</details>

#### 24. Write a query to show customer names in uppercase after removing extra spaces.

<details>

<summary>Solution</summary>

```sql
SELECT FullName,
       UPPER(TRIM(FullName)) AS CleanUpperName
FROM Customers;
```

</details>

#### 25. Write a query to show each employee email name part before `@`.

<details>

<summary>Solution</summary>

```sql
SELECT WorkEmail,
       LEFT(WorkEmail, CHARINDEX('@', WorkEmail) - 1) AS EmailUserName
FROM Employees;
```

</details>

#### 26. Which function is better when you want to join many values into one result?

<details>

<summary>Solution</summary>

Use `CONCAT()`.

It joins multiple values into one text result.

</details>
