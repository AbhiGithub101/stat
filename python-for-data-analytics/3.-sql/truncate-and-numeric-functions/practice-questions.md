---
description: >-
  practice questions on TRUNCATE, numeric functions, and data conversion in SQL
  Server
hidden: true
---

# Practice Questions

### Sample data

Use these tables for the questions on this page.

#### Create the tables

```sql
CREATE TABLE TrainingLog (
    LogID INT IDENTITY(1,1) PRIMARY KEY,
    EmployeeName VARCHAR(100),
    ModuleName VARCHAR(100),
    Score DECIMAL(5,2),
    AttemptDate DATE
);

CREATE TABLE ProductMetrics (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Price DECIMAL(10,2),
    DiscountPercent DECIMAL(5,2),
    StockQty INT,
    Rating DECIMAL(4,2),
    LengthCm DECIMAL(6,2),
    WidthCm DECIMAL(6,2),
    ProfitAmount DECIMAL(10,2),
    LaunchDateText VARCHAR(20)
);
```

#### Insert sample data

```sql
INSERT INTO TrainingLog (EmployeeName, ModuleName, Score, AttemptDate)
VALUES
('Aman Verma', 'SQL Basics', 82.50, '2026-06-01'),
('Priya Nair', 'SQL Basics', 91.00, '2026-06-02'),
('Rohan Mehta', 'Numeric Functions', 76.25, '2026-06-03'),
('Sneha Kapoor', 'Numeric Functions', 88.75, '2026-06-04'),
('Arjun Das', 'Data Conversion', 79.50, '2026-06-05');

INSERT INTO ProductMetrics (ProductID, ProductName, Price, DiscountPercent, StockQty, Rating, LengthCm, WidthCm, ProfitAmount, LaunchDateText)
VALUES
(101, 'Laptop Sleeve', 799.75, 12.50, 24, 4.35, 35.80, 25.40, 2500.00, '2026-01-15'),
(102, 'Wireless Mouse', 649.40, 8.25, 57, 4.70, 11.60, 6.20, -120.00, '2026-02-01'),
(103, 'Desk Lamp', 1250.90, 15.00, 16, 4.10, 42.50, 18.30, 870.00, '2026-02-12'),
(104, 'Notebook Set', 299.99, 5.00, 120, 3.95, 21.00, 14.80, 0.00, '2026-03-05'),
(105, 'Office Chair', 5899.55, 10.75, 9, 4.55, 110.40, 48.60, 1450.00, '2026-03-20');
```

#### Check your data

```sql
SELECT * FROM TrainingLog;
SELECT * FROM ProductMetrics;
```

Assume these tables exist:

* `TrainingLog(LogID, EmployeeName, ModuleName, Score, AttemptDate)`
* `ProductMetrics(ProductID, ProductName, Price, DiscountPercent, StockQty, Rating, LengthCm, WidthCm, ProfitAmount, LaunchDateText)`

#### 2. Write a query to remove all rows from `TrainingLog`.

<details>

<summary>Solution</summary>

```sql
TRUNCATE TABLE TrainingLog;
```

</details>

#### 3. Can `TRUNCATE TABLE` remove only selected rows?

<details>

<summary>Solution</summary>

No.

`TRUNCATE TABLE` removes all rows only.

It does not support `WHERE`.

</details>

#### Moderate

#### 4. After `TRUNCATE TABLE TrainingLog`, you insert one new row. What will the `LogID` be?

<details>

<summary>Solution</summary>

The `LogID` starts again from `1`.

That happens because `TRUNCATE` resets the `IDENTITY` value in this table.

</details>

#### 5. Write the query to insert one new row into `TrainingLog` after truncating it.

<details>

<summary>Solution</summary>

```sql
INSERT INTO TrainingLog (EmployeeName, ModuleName, Score, AttemptDate)
VALUES ('Meera Joshi', 'TRUNCATE Practice', 85.00, '2026-06-10');
```

</details>

### 2. ABS, CEILING, FLOOR, and ROUND

#### Easy

#### 1. Write a query to show the absolute value of `ProfitAmount` for each product.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       ProfitAmount,
       ABS(ProfitAmount) AS AbsoluteProfit
FROM ProductMetrics;
```

</details>

#### 2. Write a query to round each `Price` up to the next whole number.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       Price,
       CEILING(Price) AS RoundedUpPrice
FROM ProductMetrics;
```

</details>

#### 3. Write a query to round each `Price` down to the previous whole number.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       Price,
       FLOOR(Price) AS RoundedDownPrice
FROM ProductMetrics;
```

</details>

#### 4. What is the difference between `CEILING()` and `FLOOR()`?

<details>

<summary>Solution</summary>

* `CEILING()` rounds up.
* `FLOOR()` rounds down.

Example:

* `CEILING(12.1)` returns `13`
* `FLOOR(12.9)` returns `12`

</details>

#### Moderate

#### 5. Write a query to round each `Rating` to 1 decimal place.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       Rating,
       ROUND(Rating, 1) AS RoundedRating
FROM ProductMetrics;
```

</details>

#### 6. Write a query to round each `Price` to the nearest hundred.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       Price,
       ROUND(Price, -2) AS RoundedToHundred
FROM ProductMetrics;
```

</details>

### 3. POWER, SQRT, and SQUARE

#### Easy

#### 1. Write a query to show the square of `StockQty` for each product.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       StockQty,
       SQUARE(StockQty) AS StockQtySquare
FROM ProductMetrics;
```

</details>

#### 2. Write a query to show the square root of `StockQty` for each product.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       StockQty,
       SQRT(StockQty) AS StockQtyRoot
FROM ProductMetrics;
```

</details>

#### 3. Write a query to find `2` raised to the power `5`.

<details>

<summary>Solution</summary>

```sql
SELECT POWER(2, 5) AS Result;
```

</details>

#### Moderate

#### 4. Write a query to show the square of `LengthCm` for each product.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       LengthCm,
       SQUARE(LengthCm) AS LengthSquare
FROM ProductMetrics;
```

</details>

#### 5. What is the difference between `SQRT(25)` and `SQUARE(25)`?

<details>

<summary>Solution</summary>

* `SQRT(25)` returns `5`
* `SQUARE(25)` returns `625`

One finds the root.

The other multiplies the number by itself.

</details>

### 4. RAND, SIGN, and PI

#### Easy

#### 1. Write a query to generate a random decimal number.

<details>

<summary>Solution</summary>

```sql
SELECT RAND() AS RandomNumber;
```

</details>

#### 2. Write a query to show whether each `ProfitAmount` is positive, negative, or zero.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       ProfitAmount,
       SIGN(ProfitAmount) AS ProfitSign
FROM ProductMetrics;
```

`1` means positive.

`-1` means negative.

`0` means zero.

</details>

#### 3. What does `PI()` return?

<details>

<summary>Solution</summary>

`PI()` returns the value of pi.

Its value is about `3.14159265358979`.

</details>

#### Moderate

#### 4. Write a query to generate a random whole number from `1` to `50`.

<details>

<summary>Solution</summary>

```sql
SELECT FLOOR(RAND() * 50) + 1 AS RandomWholeNumber;
```

</details>

#### 5. Write a query to calculate the area of a circle with radius `6`.

<details>

<summary>Solution</summary>

```sql
SELECT PI() * SQUARE(6) AS CircleArea;
```

</details>

### 5. LOG, LOG10, SIN, COS, and TAN

#### Easy

#### 1. Write a query to find the natural log of `100`.

<details>

<summary>Solution</summary>

```sql
SELECT LOG(100) AS NaturalLogValue;
```

</details>

#### 2. Write a query to find the base-10 log of `1000`.

<details>

<summary>Solution</summary>

```sql
SELECT LOG10(1000) AS Log10Value;
```

</details>

#### 3. Write a query to find the value of `SIN(PI()/2)`.

<details>

<summary>Solution</summary>

```sql
SELECT SIN(PI() / 2) AS SinValue;
```

</details>

#### Moderate

#### 4. Write one query to show `COS(0)` and `TAN(PI()/4)`.

<details>

<summary>Solution</summary>

```sql
SELECT COS(0) AS CosValue,
       TAN(PI() / 4) AS TanValue;
```

</details>

#### 5. Why do we multiply degrees by `PI()/180` in SQL Server trigonometric functions?

<details>

<summary>Solution</summary>

SQL Server trigonometric functions use radians.

So degrees must be converted to radians first.

Formula:

```sql
Degrees * PI() / 180
```

</details>

#### 6. Write a query to find the sine of `60` degrees.

<details>

<summary>Solution</summary>

```sql
SELECT SIN(60 * PI() / 180.0) AS Sin60Degrees;
```

</details>

### 6. CAST and CONVERT

#### Easy

#### 1. Write a query to convert each `Price` into `INT` using `CAST()`.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       Price,
       CAST(Price AS INT) AS PriceAsInt
FROM ProductMetrics;
```

</details>

#### 2. Write a query to convert `LaunchDateText` into `DATE` using `CONVERT()`.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       LaunchDateText,
       CONVERT(DATE, LaunchDateText) AS LaunchDate
FROM ProductMetrics;
```

</details>

#### 3. Write a query to show only the current date from `GETDATE()`.

<details>

<summary>Solution</summary>

```sql
SELECT CAST(GETDATE() AS DATE) AS CurrentDate;
```

</details>

#### 4. Which functions can convert one data type into another in SQL Server?

<details>

<summary>Solution</summary>

Both `CAST()` and `CONVERT()` can do that.

</details>

#### Moderate

#### 5. Write a query to convert each `Price` into text.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       Price,
       CONVERT(VARCHAR(20), Price) AS PriceAsText
FROM ProductMetrics;
```

</details>

#### 6. Write a query to show `LaunchDateText` in `DD/MM/YYYY` format.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       CONVERT(VARCHAR(10), CONVERT(DATE, LaunchDateText), 103) AS LaunchDateFormatted
FROM ProductMetrics;
```

</details>

#### 7. What is one simple difference between `CAST()` and `CONVERT()`?

<details>

<summary>Solution</summary>

`CAST()` is more standard and simple.

`CONVERT()` is very useful in SQL Server when you want formatting styles, especially for dates.

</details>

### Quick challenge set

#### 1. Write a query to show `ProductName`, rounded `Price`, and rounded `Rating` together.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       ROUND(Price, 0) AS RoundedPrice,
       ROUND(Rating, 1) AS RoundedRating
FROM ProductMetrics;
```

</details>

#### 2. Write a query to show `ProductName` and absolute profit only for rows where profit is negative.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       ABS(ProfitAmount) AS AbsoluteLoss
FROM ProductMetrics
WHERE ProfitAmount < 0;
```

</details>

#### 3. Write a query to show `ProductName`, `LaunchDateText`, and the converted launch date.

<details>

<summary>Solution</summary>

```sql
SELECT ProductName,
       LaunchDateText,
       CAST(LaunchDateText AS DATE) AS LaunchDate
FROM ProductMetrics;
```

</details>

#### 4. Write a query to show the area of a circle with radius `10`, rounded to 2 decimal places.

<details>

<summary>Solution</summary>

```sql
SELECT ROUND(PI() * SQUARE(10), 2) AS CircleArea;
```

</details>
