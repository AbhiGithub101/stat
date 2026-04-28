---
hidden: true
---

# Date and Time Functions

#### What are Date & Time Functions?

Date and Time functions are **built-in SQL functions** that help you work with dates and times  like getting today's date, extracting the month from a date, calculating how many days between two dates, and more.

### 1. Getting Current Date & Time

These functions return the **current date and/or time** from the system.

#### **A. GETDATE()**

Returns the **current date and time** of the server.

```sql
SELECT GETDATE() AS CurrentDateTime;
```

**Result:**

| CurrentDateTime         |
| ----------------------- |
| 2026-04-28 18:05:24.270 |

> Most commonly used function for getting current date and time in SQL Server.

**SYSDATETIME()**

Returns the **current date and time** with **more precision** than GETDATE().

```sql
SELECT SYSDATETIME() AS CurrentDateTime;
```

**Result:**

| CurrentDateTime             |
| --------------------------- |
| 2026-04-28 18:06:49.2504413 |

**GETDATE() vs SYSDATETIME()**

|                | GETDATE()        | SYSDATETIME()              |
| -------------- | ---------------- | -------------------------- |
| Returns        | Date + Time      | Date + Time                |
| Precision      | 3 decimal places | 7 decimal places           |
| Commonly used? | Yes,most common  | Less common                |
| Use when       | General use      | When high precision needed |

#### **GETUTCDATE()**

Returns the **current UTC date and time.** UTC means Coordinated Universal Time, it is the world standard time that does not change with timezones.

```sql
SELECT GETUTCDATE() AS UTCDateTime;
```

**Result:**

| UTCDateTime             |
| ----------------------- |
| 2026-04-28 12:38:23.517 |

> If your SQL Server is in India (IST = UTC + 5:30), the UTC time will be 5 hours 30 minutes behind IST.

#### **SYSUTCDATETIME()**

Same as GETUTCDATE() but with **more precision** just like SYSDATETIME() vs GETDATE().

```sql
SELECT SYSUTCDATETIME() AS UTCDateTime;
```

**Result:**

| UTCDateTime                 |
| --------------------------- |
| 2026-04-28 12:39:26.2206027 |

**Current Date Functions**

| Function           | Returns                     | Precision        |
| ------------------ | --------------------------- | ---------------- |
| `GETDATE()`        | Current date + time (local) | 3 decimal places |
| `SYSDATETIME()`    | Current date + time (local) | 7 decimal places |
| `GETUTCDATE()`     | Current date + time (UTC)   | 3 decimal places |
| `SYSUTCDATETIME()` | Current date + time (UTC)   | 7 decimal places |

### 2. Extracting Specific Parts of a Date

Sometimes you do not need the full date,you just want the **year, month, day, hour** etc. There are two ways to do this in SQL Server.

{% tabs %}
{% tab title="First Tab" %}
**Method 1 : Using Direct Functions**

These are simple functions where each one extracts one specific part:

```sql
SELECT YEAR(GETDATE())    AS CurrentYear;
SELECT MONTH(GETDATE())   AS CurrentMonth;
SELECT DAY(GETDATE())     AS CurrentDay;
```

**Result:**

| CurrentYear | CurrentMonth | CurrentDay |
| ----------- | ------------ | ---------- |
| 2026        | 4            | 28         |



You can also use these on any date value:

```sql
SELECT YEAR('2017-04-05')   AS MatchYear;    -- Output: 2017
SELECT MONTH('2017-04-05')  AS MatchMonth;   -- Output: 4
SELECT DAY('2017-04-05')    AS MatchDay;     -- Output: 5
```
{% endtab %}

{% tab title="Second Tab" %}
**Method 2 :** **Using DATEPART()**

DATEPART is a more flexible function ,you tell it **which part** you want and **from which date.**

**Syntax:**

```sql
SELECT DATEPART(part, date);
```

| Part      | What it returns                    |
| --------- | ---------------------------------- |
| `year`    | Year number                        |
| `month`   | Month number                       |
| `day`     | Day number                         |
| `hour`    | Hour number                        |
| `minute`  | Minute number                      |
| `second`  | Second number                      |
| `weekday` | Day of week (1=Sunday, 7=Saturday) |
| `week`    | Week number of the year            |
| `quarter` | Quarter (1, 2, 3 or 4)             |

**Examples:**

```sql
SELECT DATEPART(year,    GETDATE()) AS YearPart;      -- Output: 2026
SELECT DATEPART(month,   GETDATE()) AS MonthPart;     -- Output: 4
SELECT DATEPART(day,     GETDATE()) AS DayPart;       -- Output: 28
SELECT DATEPART(hour,    GETDATE()) AS HourPart;      -- Output: 18
SELECT DATEPART(minute,  GETDATE()) AS MinutePart;    -- Output: 20
SELECT DATEPART(second,  GETDATE()) AS SecondPart;    -- Output: 18
SELECT DATEPART(weekday, GETDATE()) AS WeekDayPart;   -- Output: 3 (Tuesday)
SELECT DATEPART(week,    GETDATE()) AS WeekPart;      -- Output: 18
SELECT DATEPART(quarter, GETDATE()) AS QuarterPart;   -- Output: 2
```
{% endtab %}
{% endtabs %}

> Use direct functions for quick year/month/day. Use DATEPART when you need hour, minute, weekday, quarter etc.

### 3. Getting Names of Date Parts : DATENAME()

DATEPART gives you **numbers**  like month 3. But what if you want the actual **name**  like "April"?

That is what DATENAME() does , it returns the **name** instead of the number.

**Syntax:**

```sql
SELECT DATENAME(part, date);
```

**Examples:**

```sql
SELECT DATENAME(month,   GETDATE()) AS MonthName;    -- Output: April
SELECT DATENAME(weekday, GETDATE()) AS DayName;      -- Output: Tuesday
SELECT DATENAME(year,    GETDATE()) AS YearName;     -- Output: 2026
SELECT DATENAME(quarter, GETDATE()) AS QuarterName;  -- Output: 2
```

### 4. EOMONTH()  ( End of Month)&#x20;

EOMONTH returns the **last date of the month** for any given date.

**Syntax:**

```sql
SELECT EOMONTH(date);
```

**Examples:**

```sql
SELECT EOMONTH(GETDATE())          AS EndOfThisMonth;
-- If today is 28-April-2026 → Output: 2026-04-30

SELECT EOMONTH('2024-02-01')       AS EndOfFeb;
-- Output: 2024-02-29  (2024 is a leap year)

SELECT EOMONTH('2023-02-01')       AS EndOfFeb2023;
-- Output: 2023-02-28  (2023 is not a leap year)
```

**Result:**

| EndOfThisMonth | EndOfFeb   | EndOfFeb2023 |
| -------------- | ---------- | ------------ |
| 2026-04-30     | 2024-02-29 | 2023-02-28   |

> EOMONTH is smart enough to handle leap years automatically.

You can also get the end of **next month** by passing a second argument:

```sql
SELECT EOMONTH(GETDATE(), 1)  AS EndOfNextMonth;
-- Output: 2026-05-31

SELECT EOMONTH(GETDATE(), -1) AS EndOfLastMonth;
-- Output: 2026-03-31
```

**Real-life use:** Finding billing cycle end dates, salary processing deadlines, month end reports.

### 5. Date Calculations

{% tabs %}
{% tab title="First Tab" %}
**DATEADD() :** **Add or Subtract from a Date**

DATEADD adds or subtracts a specific amount of time from a date.

**Syntax:**

```sql
SELECT DATEADD(part, number, date);
```

* **part** → what to add -> year, month, day, hour etc
* **number** → how many to add (use negative to subtract)
* **date** → the date to add to

**Examples -> Adding:**

```sql
SELECT DATEADD(day,   7,  GETDATE()) AS After7Days;
-- Output: 2026-05-05 (7 days from today)

SELECT DATEADD(month, 3,  GETDATE()) AS After3Months;
-- Output: 2026-07-28 (3 months from today)

SELECT DATEADD(year,  1,  GETDATE()) AS After1Year;
-- Output: 2027-04-28 (1 year from today)

SELECT DATEADD(hour,  5,  GETDATE()) AS After5Hours;
-- Output: 2026-04-28 23:37:41.010
```

**Examples -> Subtracting (use negative number):**

```sql
SELECT DATEADD(day,   -7,  GETDATE()) AS Before7Days;
-- Output: 2026-04-21 (7 days before today)

SELECT DATEADD(month, -1,  GETDATE()) AS LastMonth;
-- Output: 2026-03-28

SELECT DATEADD(year,  -1,  GETDATE()) AS LastYear;
-- Output: 2025-04-28
```

> **Real-life use:** Calculating expiry dates, due dates, subscription end dates, reminder dates.
{% endtab %}

{% tab title="Second Tab" %}
**DATEDIFF() -> Difference Between Two Dates**

DATEDIFF calculates **how much time is between two dates.**

**Syntax:**

```sql
SELECT DATEDIFF(part, start_date, end_date);
```

* **part** → what unit to measure in (day, month, year, hour etc)
* **start\_date** → the earlier date
* **end\_date** → the later date

**Examples:**

```sql
-- How many days between two dates?
SELECT DATEDIFF(day, '2024-01-01', '2024-03-25') AS DaysDiff;
-- Output: 84

-- How many months between two dates?
SELECT DATEDIFF(month, '2024-01-01', '2024-03-25') AS MonthsDiff;
-- Output: 2

-- How many years between two dates?
SELECT DATEDIFF(year, '2000-08-15', GETDATE()) AS YearsDiff;
-- Output: 23

-- How many days since IPL 2017 started?
SELECT DATEDIFF(day, '2017-04-05', GETDATE()) AS DaysSinceIPL2017;
-- Output: 2546
```

> **Real-life use:** Calculating age, number of days since joining, days remaining for an event, how long a project took.

**Calculating Age using DATEDIFF:**

```sql
SELECT DATEDIFF(year, '2000-08-15', GETDATE()) AS Age;
-- Output: 23
```
{% endtab %}
{% endtabs %}

### 6. Converting String to Date

Sometimes dates come in as plain text  like `'25-03-2024'` or `'March 25 2024'`  and you need to convert them into a proper date format SQL understands.

Use **CONVERT** or **CAST** for this:

{% tabs %}
{% tab title="First Tab" %}
**Using CAST:**

```sql
SELECT CAST('2024-03-25' AS DATE) AS CastedDate;
-- Output: 2024-03-25

SELECT CAST('2024-03-25 14:30:00' AS DATETIME) AS CastedDateTime;
-- Output: 2024-03-25 14:30:00.000
```
{% endtab %}

{% tab title="Second Tab" %}
**Using CONVERT:**

```sql
SELECT CONVERT(DATE, '2024-03-25') AS ConvertedDate;
-- Output: 2024-03-25

SELECT CONVERT(DATETIME, '2024-03-25 14:30:00') AS ConvertedDateTime;
-- Output: 2024-03-25 14:30:00.000
```
{% endtab %}
{% endtabs %}

### 7. Converting Date to Different Styles

SQL Server lets you display dates in **many different formats** using CONVERT with a style number.

**Syntax:**

```sql
SELECT CONVERT(VARCHAR, date, style_number);
```

| Style Number | Format               | Example Output       |
| ------------ | -------------------- | -------------------- |
| `103`        | DD/MM/YYYY           | 25/03/2024           |
| `101`        | MM/DD/YYYY           | 03/25/2024           |
| `104`        | DD.MM.YYYY           | 25.03.2024           |
| `105`        | DD-MM-YYYY           | 25-03-2024           |
| `106`        | DD Mon YYYY          | 25 Mar 2024          |
| `107`        | Mon DD, YYYY         | Mar 25, 2024         |
| `110`        | MM-DD-YYYY           | 03-25-2024           |
| `111`        | YYYY/MM/DD           | 2024/03/25           |
| `112`        | YYYYMMDD             | 20240325             |
| `113`        | DD Mon YYYY HH:MM:SS | 25 Mar 2024 14:35:22 |

**Examples:**

```sql
SELECT CONVERT(VARCHAR, GETDATE(), 103) AS IndianFormat;
-- Output: 28/04/2026

SELECT CONVERT(VARCHAR, GETDATE(), 107) AS ReadableFormat;
-- Output: Apr 28, 2026

SELECT CONVERT(VARCHAR, GETDATE(), 112) AS CompactFormat;
-- Output: 20260428

SELECT CONVERT(VARCHAR, GETDATE(), 106) AS LongFormat;
-- Output: 28 Apr 2026
```

**Real-life use:** Displaying dates in reports the way users expect ,Indian format DD/MM/YYYY is style 103, American format MM/DD/YYYY is style 101.



**Coming Up Next:** Ever wondered how to wipe an entire table in one shot (faster than DELETE) ? Or how to round off numbers, find absolute values and do math directly in SQL? That is exactly what we cover next!
