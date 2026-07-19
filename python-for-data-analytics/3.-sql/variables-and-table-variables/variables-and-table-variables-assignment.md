---
description: Practice SQL Server variables and table variables.
hidden: true
---

# Variables & Table Variables Assignment

### Practice dataset

```sql
CREATE TABLE Sales (
    SaleID INT,
    SalespersonName VARCHAR(100),
    Region VARCHAR(50),
    Amount DECIMAL(10, 2)
);

INSERT INTO Sales (SaleID, SalespersonName, Region, Amount)
VALUES
(101, 'Aditi Sharma', 'North', 12500.75),
(102, 'Rohan Mehta', 'North', 9800.00),
(103, 'Neha Kapoor', 'North', 11400.50),
(104, 'Aditi Sharma', 'North', 10500.00),
(105, 'Kabir Singh', 'North', 13200.25),
(106, 'Rohan Mehta', 'North', 15000.00),
(201, 'Isha Nair', 'South', 8200.00),
(202, 'Vikram Rao', 'South', 9100.50),
(203, 'Isha Nair', 'South', 7600.00),
(204, 'Sara Khan', 'West', 14300.00),
(205, 'Arjun Das', 'West', 11800.00),
(206, 'Sara Khan', 'West', 6700.00);
```

### Variables

#### 1. Declare an integer variable named `@CustomerCount`.

<details>

<summary>Solution</summary>

```sql
DECLARE @CustomerCount INT;
```

`DECLARE` creates the variable. SQL Server variables start with `@`.

</details>

#### 2. Declare a variable that can store the name `Aditi Sharma`.

<details>

<summary>Solution</summary>

```sql
DECLARE @CustomerName VARCHAR(100);
```

`VARCHAR(100)` can store text up to 100 characters.

</details>

#### 3. What value does a declared variable contain before assignment?

* A. `0`
* B. An empty string
* C. `NULL`
* D. The column default

<details>

<summary>Solution</summary>

**C. `NULL`**

Declaring a variable does not assign a value.

</details>

#### 4. Assign  `12500.75`  to a decimal variable named `@MonthlyTarget`. Then display it as `MonthlyTarget`.

<details>

<summary>Solution</summary>

```sql
DECLARE @MonthlyTarget DECIMAL(10, 2);
SET @MonthlyTarget = 12500.75;

SELECT @MonthlyTarget AS MonthlyTarget;
```

</details>

#### 5. Complete the statement to store `45` in `@OpenTickets`.

```sql
DECLARE @OpenTickets INT;
_____ @OpenTickets = 45;
```

<details>

<summary>Solution</summary>

```sql
SET @OpenTickets = 45;
```

`SET` assigns one value to a variable.

</details>

#### 6. Declare `@ReportDate` as a `DATE` variable. Store `2026-07-14` in it and display it.

<details>

<summary>Solution</summary>

```sql
DECLARE @ReportDate DATE;
SET @ReportDate = '2026-07-14';

SELECT @ReportDate AS ReportDate;
```

</details>

#### 7. A manager needs the amount from `SaleID = 101`. Store it in `@SaleAmount` and display it.

<details>

<summary>Solution</summary>

```sql
DECLARE @SaleAmount DECIMAL(10, 2);

SELECT @SaleAmount = Amount
FROM Sales
WHERE SaleID = 101;

SELECT @SaleAmount AS SaleAmount;
```

The query result is assigned directly to the variable.

</details>

#### 8. Which statement can assign values to multiple variables in one query?

* A. `CREATE`
* B. `SELECT`
* C. `DROP`
* D. `TRUNCATE`

<details>

<summary>Solution</summary>

**B. `SELECT`**

`SELECT` can assign several variables from one query.

</details>

#### 9. Store the highest and lowest sale amounts from `Sales` in separate variables. Display both values.

<details>

<summary>Solution</summary>

```sql
DECLARE @HighestSale DECIMAL(10, 2);
DECLARE @LowestSale DECIMAL(10, 2);

SELECT @HighestSale = MAX(Amount),
       @LowestSale = MIN(Amount)
FROM Sales;

SELECT @HighestSale AS HighestSale,
       @LowestSale AS LowestSale;
```

</details>

#### 10. `SET` and `SELECT` can both assign a value to a variable. True or False?

<details>

<summary>Solution</summary>

**True.**

Both statements can assign variable values.

</details>

#### 11. Store the number of sales in the `North` region in `@NorthSaleCount`. Display the result.

<details>

<summary>Solution</summary>

```sql
DECLARE @NorthSaleCount INT;

SELECT @NorthSaleCount = COUNT(*)
FROM Sales
WHERE Region = 'North';

SELECT @NorthSaleCount AS NorthSaleCount;
```

</details>

#### 12. A report needs the salesperson name from `SaleID = 205`. Write the query using `@SalespersonName`.

<details>

<summary>Solution</summary>

```sql
DECLARE @SalespersonName VARCHAR(100);

SELECT @SalespersonName = SalespersonName
FROM Sales
WHERE SaleID = 205;

SELECT @SalespersonName AS SalespersonName;
```

</details>

#### 13. Which declaration is valid in SQL Server?

* A. `DECLARE Total INT;`
* B. `DECLARE @Total INT;`
* C. `VARIABLE @Total INT;`
* D. `SET @Total INT;`

<details>

<summary>Solution</summary>

**B. `DECLARE @Total INT;`**

A SQL Server variable starts with `@` and uses `DECLARE`.

</details>

### Table variables

#### 14. Declare a table variable named `@DailySales` with `SaleID` as `INT` and `Amount` as `DECIMAL(10, 2)`.

<details>

<summary>Solution</summary>

```sql
DECLARE @DailySales TABLE (
    SaleID INT,
    Amount DECIMAL(10, 2)
);
```

</details>

#### 15. Which keyword declares a table variable?

* A. `TABLE`
* B. `DECLARE`
* C. `INSERT`
* D. `SELECT`

<details>

<summary>Solution</summary>

**B. `DECLARE`**

Use `DECLARE @VariableName TABLE (...)`.

</details>

#### 16. Create `@SupportQueue` with `TicketID INT` and `Priority VARCHAR(20)`.  Insert one row: `501, 'High'`  and Display the rows.

<details>

<summary>Solution</summary>

```sql
DECLARE @SupportQueue TABLE (
    TicketID INT,
    Priority VARCHAR(20)
);

INSERT INTO @SupportQueue (TicketID, Priority)
VALUES (501, 'High');

SELECT *
FROM @SupportQueue;
```

</details>

#### 17. A table variable can hold only one row. True or False?

<details>

<summary>Solution</summary>

**False.**

A table variable can hold multiple rows.

</details>

#### 18. Create `@RegionalSales` with `Region VARCHAR(50)` and `TotalSales INT`. Insert the sales count for each region from `Sales`.

<details>

<summary>Solution</summary>

```sql
DECLARE @RegionalSales TABLE (
    Region VARCHAR(50),
    TotalSales INT
);

INSERT INTO @RegionalSales (Region, TotalSales)
SELECT Region, COUNT(*)
FROM Sales
GROUP BY Region;

SELECT *
FROM @RegionalSales;
```

</details>

#### 19. Complete the declaration.

```sql
DECLARE @TopRegions _____ (
    Region VARCHAR(50),
    SaleCount INT
);
```

<details>

<summary>Solution</summary>

```sql
DECLARE @TopRegions TABLE (
    Region VARCHAR(50),
    SaleCount INT
);
```

</details>

#### 20. Create `@TopRegions`. Store regions with more than five sales. Include each region and its sale count.

<details>

<summary>Solution</summary>

```sql
DECLARE @TopRegions TABLE (
    Region VARCHAR(50),
    SaleCount INT
);

INSERT INTO @TopRegions (Region, SaleCount)
SELECT Region, COUNT(*)
FROM Sales
GROUP BY Region
HAVING COUNT(*) > 5;

SELECT *
FROM @TopRegions;
```

`HAVING` filters grouped results before they are stored.

</details>

#### 21. Which statement adds rows to `@DailySales`?

* A. `INSERT INTO @DailySales ...`
* B. `DECLARE INTO @DailySales ...`
* C. `SET INTO @DailySales ...`
* D. `CREATE INTO @DailySales ...`

<details>

<summary>Solution</summary>

**A. `INSERT INTO @DailySales ...`**

Use `INSERT INTO` to add rows.

</details>

#### 22. Create `@HighValueSales` with `SalespersonName` and `Amount`. Store sales where `Amount` is greater than `10000`. Display the table variable.

<details>

<summary>Solution</summary>

```sql
DECLARE @HighValueSales TABLE (
    SalespersonName VARCHAR(100),
    Amount DECIMAL(10, 2)
);

INSERT INTO @HighValueSales (SalespersonName, Amount)
SELECT SalespersonName, Amount
FROM Sales
WHERE Amount > 10000;

SELECT *
FROM @HighValueSales;
```

</details>

#### 23. Create `@RegionTotals` with `Region` and `TotalAmount`. Store the total sales amount by region. Keep only regions above `50000`.

<details>

<summary>Solution</summary>

```sql
DECLARE @RegionTotals TABLE (
    Region VARCHAR(50),
    TotalAmount DECIMAL(10, 2)
);

INSERT INTO @RegionTotals (Region, TotalAmount)
SELECT Region, SUM(Amount)
FROM Sales
GROUP BY Region
HAVING SUM(Amount) > 50000;

SELECT *
FROM @RegionTotals;
```

</details>

#### 24. Build `@SalesSummary` with `Region`, `HighestAmount`, and `LowestAmount`. Populate it from `Sales` and display the result.

<details>

<summary>Solution</summary>

```sql
DECLARE @SalesSummary TABLE (
    Region VARCHAR(50),
    HighestAmount DECIMAL(10, 2),
    LowestAmount DECIMAL(10, 2)
);

INSERT INTO @SalesSummary (Region, HighestAmount, LowestAmount)
SELECT Region, MAX(Amount), MIN(Amount)
FROM Sales
GROUP BY Region;

SELECT *
FROM @SalesSummary;
```

</details>

#### 25. Which statement correctly reads every row from a table variable named `@Inventory`?

* A. `SELECT * FROM Inventory;`
* B. `SELECT * FROM @Inventory;`
* C. `SELECT @Inventory;`
* D. `DISPLAY @Inventory;`

<details>

<summary>Solution</summary>

**B. `SELECT * FROM @Inventory;`**

A table variable name includes `@`.

</details>
