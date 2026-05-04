# Truncate and Numeric Functions

## What is TRUNCATE?

TRUNCATE is used to **delete all rows from a table instantly** in one shot. It removes all the data but **keeps the table structure** intact.

Think of it like this: You have a whiteboard full of writing ,TRUNCATE erases everything on it completely, but the whiteboard itself is still there. You can write on it again.

#### Syntax

```sql
TRUNCATE TABLE TableName;
```

**Example:**

```sql
TRUNCATE TABLE Employee;
```

**Before TRUNCATE:**

| ID | FullName     | Department |
| -- | ------------ | ---------- |
| 1  | Rahul Sharma | IT         |
| 2  | Priya Verma  | HR         |
| 3  | Amit Gupta   | Finance    |
| 4  | Sneha Patil  | IT         |
| 5  | Ravi Shankar | HR         |

**After TRUNCATE:**

| ID                  | FullName | Department |
| ------------------- | -------- | ---------- |
| _(empty — no rows)_ |          |            |

> The table still exists ,all columns are still there. Only the data is gone.

#### TRUNCATE vs DELETE&#x20;

|                     | DELETE                            | TRUNCATE                      |
| ------------------- | --------------------------------- | ----------------------------- |
| Removes             | Specific rows or all rows         | Always all rows               |
| WHERE clause?       | Yes , can delete specific rows    |  No , removes everything      |
| Speed               | Slower , removes row by row       | Faster , removes all at once  |
| Can be rolled back? |  Yes                              |  No in most cases             |
| Resets IDENTITY?    | No , ID continues from last value |  Yes, ID resets back to start |

**IDENTITY reset example:**

```sql
-- After inserting 5 employees, last ID was 5
-- Now DELETE all rows and insert again
DELETE FROM Employee;
INSERT INTO Employee (FullName) VALUES ('New Person');
-- New ID will be 6 -- continues from where it left off

-- Now TRUNCATE and insert again
TRUNCATE TABLE Employee;
INSERT INTO Employee (FullName) VALUES ('New Person');
-- New ID will be 1 -- resets back to st
```

**When to use which?**

| Situation                              | Use                   |
| -------------------------------------- | --------------------- |
| Want to delete specific rows           | `DELETE` with `WHERE` |
| Want to delete all rows but keep table | `TRUNCATE`            |
| Want to reset IDENTITY counter         | `TRUNCATE`            |
| Want to be able to undo the delete     | `DELETE`              |

## Numeric Functions

Numeric functions are **built-in SQL functions** that help you perform mathematical operations on numbers  like rounding, finding square roots, generating random numbers and more.

Think of it like a **calculator built into SQL** , you can do math directly in your queries.

### 1. ABS() : Absolute Value

ABS returns the **positive version** of any number , it removes the negative sign if there is one.

```sql
SELECT ABS(-150)  AS Result;   -- Output: 150
SELECT ABS(150)   AS Result;   -- Output: 150
SELECT ABS(-99.5) AS Result;   -- Output: 99.5
SELECT ABS(0)     AS Result;   -- Output: 0
```

**Real-life use:** Calculating the difference between two values regardless of which is larger — like finding the temperature difference between two days.

```sql
SELECT ABS(45 - 80) AS Difference;
-- Output: 35  (not -35)
```

### 2. CEILING() : Round Up&#x20;

CEILING always rounds a decimal number **up to the next whole number** no matter how small the decimal part is.

```sql
SELECT CEILING(4.1)  AS Result;   -- Output: 5
SELECT CEILING(4.9)  AS Result;   -- Output: 5
SELECT CEILING(4.0)  AS Result;   -- Output: 4
SELECT CEILING(-4.3) AS Result;   -- Output: -4
```

**Real-life use:** Calculating how many buses are needed for a trip , if there are 41 students and each bus holds 10, you need CEILING(41/10) = 5 buses. You cannot have half a bus.

```sql
SELECT CEILING(41.0 / 10) AS BusesNeeded;
-- Output: 5
```

### 3. FLOOR() : Round Down

FLOOR always rounds a decimal number **down to the previous whole number** ,opposite of CEILING.

```sql
SELECT FLOOR(4.9)  AS Result;   -- Output: 4
SELECT FLOOR(4.1)  AS Result;   -- Output: 4
SELECT FLOOR(4.0)  AS Result;   -- Output: 4
SELECT FLOOR(-4.3) AS Result;   -- Output: -5
```

**Real-life use:** Calculating how many complete boxes you can fill , if you have 47 items and each box holds 10, FLOOR(47/10) = 4 complete boxes.

```sql
SELECT FLOOR(47.0 / 10) AS CompleteBoxes;
-- Output: 4
```

### 4. ROUND()  : Round to Specific Decimal Places

ROUND rounds a number to a **specified number of decimal places.**

**Syntax:**

```sql
SELECT ROUND(number, decimal_places);
```

```sql
SELECT ROUND(4.4567, 2)  AS Result;   -- Output: 4.46
SELECT ROUND(4.4567, 1)  AS Result;   -- Output: 4.5
SELECT ROUND(4.4567, 0)  AS Result;   -- Output: 4.0
SELECT ROUND(4.5567, 0)  AS Result;   -- Output: 5.0
SELECT ROUND(156.78, -2) AS Result;   -- Output: 200.00
```

> Negative decimal places round to the left of the decimal point  `-2` rounds to nearest hundred.

**Real-life use:** Rounding off prices, exam scores, financial calculations.

```sql
SELECT ROUND(1299.5678, 2) AS Price;
-- Output: 1299.57
```

### 5. POWER() : Raise to a Power

POWER raises a number **to the power of** another number.

**Syntax:**

```sql
SELECT POWER(number, power);
```

```sql
SELECT POWER(2, 10) AS Result;   -- Output: 1024  (2 to the power 10)
SELECT POWER(3, 3)  AS Result;   -- Output: 27    (3 to the power 3)
SELECT POWER(5, 2)  AS Result;   -- Output: 25    (5 squared)
```

**Real-life use:** Compound interest calculations, exponential growth formulas.

### 6. SQRT() : Square Root

SQRT returns the **square root** of a number.

```sql
SELECT SQRT(25)  AS Result;   -- Output: 5
SELECT SQRT(144) AS Result;   -- Output: 12
SELECT SQRT(2)   AS Result;   -- Output: 1.4142135623731
```

> The number inside SQRT must always be **positive** ,square root of a negative number is not possible and will give an error.

### 7. SQUARE() : Square of a Number

SQUARE returns the **square of a number** , the number multiplied by itself.

```sql
SELECT SQUARE(5)   AS Result;   -- Output: 25
SELECT SQUARE(12)  AS Result;   -- Output: 144
SELECT SQUARE(1.5) AS Result;   -- Output: 2.25
```

**SQRT vs SQUARE**

| Function    | What it does | Example | Output |
| ----------- | ------------ | ------- | ------ |
| `SQRT(25)`  | Square root  | √25     | 5      |
| `SQUARE(5)` | Square       | 5²      | 25     |

> SQRT and SQUARE are opposites of each other — `SQUARE(SQRT(25))` gives back 25.

### 8. RAND() : Random Number

RAND generates a **random decimal number between 0 and 1** every time it runs.

```sql
SELECT RAND() AS RandomNumber;
-- Output: 0.7184930124  (different every time)
```

**Random number between 1 and 100:**

To get a random whole number between 1 and 100 use this formula:

```sql
SELECT FLOOR(RAND() * 100) + 1 AS RandomNumber;
-- Output: any number between 1 and 100
```

**How this works:**

* `RAND()` → gives 0 to 0.999...
* `RAND() * 100` → gives 0 to 99.999...
* `FLOOR(RAND() * 100)` → gives 0 to 99
* `FLOOR(RAND() * 100) + 1` → gives 1 to 100

**Real-life use:** Generating OTPs, random sampling, lottery systems, test data generation.

### 9. SIGN() : Sign of a Number

SIGN tells you whether a number is **positive, negative or zero** , it returns 1, -1 or 0.

```sql
SELECT SIGN(150)   AS Result;   -- Output:  1  (positive)
SELECT SIGN(-150)  AS Result;   -- Output: -1  (negative)
SELECT SIGN(0)     AS Result;   -- Output:  0  (zero)
```

**Real-life use:** Checking if a transaction is a credit or debit, checking if profit or loss.

```sql
SELECT SIGN(ProfitAmount) AS ProfitOrLoss;
--  1 = Profit
-- -1 = Loss
--  0 = Breakeven
```

### 10. PI() : Value of Pi

PI() returns the mathematical value of **π (Pi).**

```sql
SELECT PI() AS PiValue;
-- Output: 3.14159265358979
```

**Real-life use:** Calculating area or circumference of circular fields, tanks, pipes.

```sql
-- Area of a circle with radius 7
SELECT PI() * SQUARE(7) AS CircleArea;
-- Output: 153.938040025...
```

### 11. LOG() and LOG10()

These return the **logarithm** of a number.

```sql
SELECT LOG(100)   AS NaturalLog;    -- Natural log (base e) → Output: 4.60517...
SELECT LOG10(100) AS Log10;         -- Log base 10          → Output: 2
SELECT LOG10(1000) AS Log10;        -- Log base 10          → Output: 3
```

> `LOG()` = natural logarithm (base e = 2.718...) `LOG10()` = common logarithm (base 10) , easier to understand

### 12. SIN(), COS(), TAN() :  Trigonometric Functions

These are trigonometry functions.

> SQL uses **radians** not degrees. To convert degrees to radians multiply by `PI()/180`.

```sql
SELECT SIN(PI()/2)  AS SinResult;   -- Output: 1      (sin 90°)
SELECT COS(0)       AS CosResult;   -- Output: 1      (cos 0°)
SELECT TAN(PI()/4)  AS TanResult;   -- Output: 1      (tan 45°)
```

### 13. Data Conversion Functions

These functions are used to **convert one data type into another.**

{% tabs %}
{% tab title="First Tab" %}
**CAST()**

```sql
SELECT CAST(99.99 AS INT)          AS Result;   -- Output: 99
SELECT CAST(99 AS DECIMAL(5,2))    AS Result;   -- Output: 99.00
SELECT CAST('2024-03-25' AS DATE)  AS Result;   -- Output: 2024-03-25
SELECT CAST(GETDATE() AS DATE)     AS Result;   -- Output: 2024-03-25
```
{% endtab %}

{% tab title="Second Tab" %}
**CONVERT()**

```sql
SELECT CONVERT(INT, 99.99)         AS Result;   -- Output: 99
SELECT CONVERT(VARCHAR, 12345)     AS Result;   -- Output: '12345'
SELECT CONVERT(DATE, '2024-03-25') AS Result;   -- Output: 2024-03-25
```
{% endtab %}
{% endtabs %}



> **Up Next:** Ever wondered how to combine data from two different tables into one result? Next module we dive into **JOINS** , one of the most powerful and most used concepts in SQL. We will cover INNER JOIN, LEFT JOIN, RIGHT JOIN and more using our matches and deliveries tables!
