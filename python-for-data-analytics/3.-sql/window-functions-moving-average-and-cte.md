# Window Functions , Moving Average & CTE

#### Our Tables for this Module

**Employee Table:**

```sql
CREATE TABLE Employee (
    ID         INT PRIMARY KEY,
    FullName   VARCHAR(100),
    Department VARCHAR(50),
    Salary     DECIMAL(10,2),
    City       VARCHAR(50)
);

INSERT INTO Employee VALUES (1,  'Rahul Sharma',  'IT',      50000, 'Delhi');
INSERT INTO Employee VALUES (2,  'Priya Verma',   'HR',      45000, 'Mumbai');
INSERT INTO Employee VALUES (3,  'Amit Gupta',    'Finance', 60000, 'Delhi');
INSERT INTO Employee VALUES (4,  'Sneha Patil',   'IT',      55000, 'Pune');
INSERT INTO Employee VALUES (5,  'Ravi Shankar',  'HR',      48000, 'Mumbai');
INSERT INTO Employee VALUES (6,  'Neha Singh',    'Finance', 70000, 'Delhi');
INSERT INTO Employee VALUES (7,  'Arjun Mehta',   'IT',      42000, 'Pune');
INSERT INTO Employee VALUES (8,  'Kavya Reddy',   'HR',      65000, 'Hyderabad');
INSERT INTO Employee VALUES (9,  'Vikram Das',    'Finance', 60000, 'Delhi');
INSERT INTO Employee VALUES (10, 'Pooja Nair',    'IT',      55000, 'Mumbai');
```

## WINDOW FUNCTIONS

#### What is a Window Function?

A Window Function performs a **calculation across a set of rows** that are related to the current row without collapsing them into groups like GROUP BY does.

Think of it like looking through a **moving window** on a train:

* You can see multiple rows outside
* But you are still sitting in your own seat
* Each row keeps its own identity

**The Problem with GROUP BY:**

```sql
-- GROUP BY collapses rows — you lose individual details
SELECT Department, AVG(Salary)
FROM Employee
GROUP BY Department;
```

| Department | AVG(Salary) |
| ---------- | ----------- |
| IT         | 50500       |
| HR         | 52666       |
| Finance    | 63333       |

> Individual employee rows are gone ,you only see department totals.

**Window Function keeps all rows:**

```sql
-- Window function — keeps every row AND adds calculation
SELECT FullName, Department, Salary,
       AVG(Salary) OVER (PARTITION BY Department) AS DeptAvgSalary
FROM Employee;
```

| FullName     | Department | Salary | DeptAvgSalary |
| ------------ | ---------- | ------ | ------------- |
| Rahul Sharma | IT         | 50000  | 50500         |
| Sneha Patil  | IT         | 55000  | 50500         |
| Arjun Mehta  | IT         | 42000  | 50500         |
| Pooja Nair   | IT         | 55000  | 50500         |
| Priya Verma  | HR         | 45000  | 52666         |
| Ravi Shankar | HR         | 48000  | 52666         |
| Kavya Reddy  | HR         | 65000  | 52666         |
| Amit Gupta   | Finance    | 60000  | 63333         |
| Neha Singh   | Finance    | 70000  | 63333         |
| Vikram Das   | Finance    | 60000  | 63333         |

> Every row is still there AND each row knows its department average. This is the power of window functions.

#### The OVER() Clause&#x20;

Every window function uses the **OVER()** clause ,it defines the "window" of rows to calculate over.

```sql
FunctionName() OVER (
    PARTITION BY column    -- divide rows into groups
    ORDER BY column        -- sort within each group
)
```

| Part           | What it does                              | Required?           |
| -------------- | ----------------------------------------- | ------------------- |
| `PARTITION BY` | Divides rows into groups like departments | Optional            |
| `ORDER BY`     | Sorts rows within each partition          | Depends on function |

**Visual Diagram of OVER() Clause:**

```
All Rows:
┌────────────────────────────────────────┐
│ Rahul    │ IT      │ 50000             │
│ Sneha    │ IT      │ 55000             │
│ Arjun    │ IT      │ 42000             │
│ Pooja    │ IT      │ 55000             │
│ Priya    │ HR      │ 45000             │
│ Ravi     │ HR      │ 48000             │
│ Kavya    │ HR      │ 65000             │
│ Amit     │ Finance │ 60000             │
│ Neha     │ Finance │ 70000             │
│ Vikram   │ Finance │ 60000             │
└────────────────────────────────────────┘

After PARTITION BY Department:
┌─────────────────┐ ┌──────────────────┐ ┌──────────────────┐
│   IT Window     │ │   HR Window      │ │ Finance Window   │
│ Rahul  │ 50000  │ │ Priya  │ 45000  │ │ Amit   │ 60000  │
│ Sneha  │ 55000  │ │ Ravi   │ 48000  │ │ Neha   │ 70000  │
│ Arjun  │ 42000  │ │ Kavya  │ 65000  │ │ Vikram │ 60000  │
│ Pooja  │ 55000  │ └──────────────────┘ └──────────────────┘
└─────────────────┘
Window function runs separately on each partition
```

### 1. ROW\_NUMBER()

ROW\_NUMBER assigns a **unique sequential number** to each row  1, 2, 3, 4... No ties ,every row gets a different number.

Think of it like giving **queue numbers** at a bank ,everyone gets a unique number regardless of anything.

**Syntax:**

```sql
SELECT FullName, Department, Salary,
       ROW_NUMBER() OVER (ORDER BY Salary DESC) AS RowNum
FROM Employee;
```

**Result:**

| FullName     | Department | Salary | RowNum |
| ------------ | ---------- | ------ | ------ |
| Neha Singh   | Finance    | 70000  | 1      |
| Kavya Reddy  | HR         | 65000  | 2      |
| Amit Gupta   | Finance    | 60000  | 3      |
| Vikram Das   | Finance    | 60000  | 4      |
| Sneha Patil  | IT         | 55000  | 5      |
| Pooja Nair   | IT         | 55000  | 6      |
| Rahul Sharma | IT         | 50000  | 7      |
| Ravi Shankar | HR         | 48000  | 8      |
| Priya Verma  | HR         | 45000  | 9      |
| Arjun Mehta  | IT         | 42000  | 10     |

> Notice Amit and Vikram both have salary 60000 but ROW\_NUMBER gives them 3 and 4 ,no ties allowed.

### 2. RANK()

RANK assigns a rank to each row but if two rows have the **same value they get the same rank** and the next rank is skipped.

Think of it like a **sports competition** ,if two players tie for 1st place, both get rank 1 and rank 2 is skipped  and next rank is 3.

**Visual of RANK vs ROW\_NUMBER:**

```
Salary   ROW_NUMBER    RANK
70000        1          1
65000        2          2
60000        3          3   ← tie
60000        4          3   ← tie (same rank)
55000        5          5   ← 4 is skipped!
55000        6          5   ← tie
50000        7          7   ← 6 is skipped!
```

**Syntax:**

```sql
SELECT FullName, Department, Salary,
       RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employee;
```

**Result:**

| FullName     | Department | Salary | SalaryRank |
| ------------ | ---------- | ------ | ---------- |
| Neha Singh   | Finance    | 70000  | 1          |
| Kavya Reddy  | HR         | 65000  | 2          |
| Amit Gupta   | Finance    | 60000  | 3          |
| Vikram Das   | Finance    | 60000  | 3          |
| Sneha Patil  | IT         | 55000  | 5          |
| Pooja Nair   | IT         | 55000  | 5          |
| Rahul Sharma | IT         | 50000  | 7          |
| Ravi Shankar | HR         | 48000  | 8          |
| Priya Verma  | HR         | 45000  | 9          |
| Arjun Mehta  | IT         | 42000  | 10         |

> Amit and Vikram both get rank 3. Rank 4 is skipped. Sneha and Pooja both get rank 5. Rank 6 is skipped.

### 3. DENSE\_RANK()

DENSE\_RANK is same as RANK but it **does NOT skip ranks** after a tie. Ranks are always consecutive.

Think of it like **exam results** ,if two students tie for 3rd place both get rank 3 and next student gets rank 4, not 5.

**Visual of All Three Compared:**

```
Salary   ROW_NUMBER    RANK    DENSE_RANK
70000        1          1          1
65000        2          2          2
60000        3          3          3   ← tie
60000        4          3          3   ← tie
55000        5          5          4   ← no skip!
55000        6          5          4   ← tie
50000        7          7          5   ← no skip!
48000        8          8          6
45000        9          9          7
42000       10         10          8
```

**Syntax:**

```sql
SELECT FullName, Department, Salary,
       ROW_NUMBER()  OVER (ORDER BY Salary DESC) AS RowNum,
       RANK()        OVER (ORDER BY Salary DESC) AS RankNum,
       DENSE_RANK()  OVER (ORDER BY Salary DESC) AS DenseRankNum
FROM Employee;
```

**Result:**

| FullName     | Salary | RowNum | RankNum | DenseRankNum |
| ------------ | ------ | ------ | ------- | ------------ |
| Neha Singh   | 70000  | 1      | 1       | 1            |
| Kavya Reddy  | 65000  | 2      | 2       | 2            |
| Amit Gupta   | 60000  | 3      | 3       | 3            |
| Vikram Das   | 60000  | 4      | 3       | 3            |
| Sneha Patil  | 55000  | 5      | 5       | 4            |
| Pooja Nair   | 55000  | 6      | 5       | 4            |
| Rahul Sharma | 50000  | 7      | 7       | 5            |
| Ravi Shankar | 48000  | 8      | 8       | 6            |
| Priya Verma  | 45000  | 9      | 9       | 7            |
| Arjun Mehta  | 42000  | 10     | 10      | 8            |

## &#x20;MOVING AVERAGE

#### What is Moving Average?

A Moving Average calculates the **average of a specific number of rows** around the current row not the whole table, just a sliding window of rows.

Think of it like a **weather forecast** instead of showing today's temperature alone, they show the average of last 3 days to smooth out sudden changes.

**Visual Diagram:**

```
Ball  Runs   Moving Avg (last 3 balls)
 1     0      0           ← only 1 ball so far
 2     0      0           ← only 2 balls so far
 3     4      1.33        ← avg of balls 1,2,3
 4     0      1.33        ← avg of balls 2,3,4
 5     2      2.00        ← avg of balls 3,4,5
 6     0      0.67        ← avg of balls 4,5,6
 7     1      1.00        ← avg of balls 5,6,7
```

We will use a simple **DailySales** table :&#x20;

```sql
CREATE TABLE DailySales (
    DayNumber  INT,
    SaleAmount INT
);

INSERT INTO DailySales VALUES (1,  100);
INSERT INTO DailySales VALUES (2,  200);
INSERT INTO DailySales VALUES (3,  150);
INSERT INTO DailySales VALUES (4,  300);
INSERT INTO DailySales VALUES (5,  250);
INSERT INTO DailySales VALUES (6,  400);
INSERT INTO DailySales VALUES (7,  350);
INSERT INTO DailySales VALUES (8,  500);
INSERT INTO DailySales VALUES (9,  450);
INSERT INTO DailySales VALUES (10, 600);
```

| DayNumber | SaleAmount |
| --------- | ---------- |
| 1         | 100        |
| 2         | 200        |
| 3         | 150        |
| 4         | 300        |
| 5         | 250        |
| 6         | 400        |
| 7         | 350        |
| 8         | 500        |
| 9         | 450        |
| 10        | 600        |

### 1. Moving Average

Moving average smooths out the data by averaging over a sliding window of rows.

**Example :** **3 Day Moving Average:**

```sql
SELECT DayNumber,
       SaleAmount,
       AVG(CAST(SaleAmount AS DECIMAL(10,2)))
       OVER (
           ORDER BY DayNumber
           ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
       ) AS MovingAvg3Days
FROM DailySales;
```

**How it calculates step by step:**

```
Day 1: Only 1 row available
       AVG(100) = 100.00

Day 2: Only 2 rows available
       AVG(100, 200) = 150.00

Day 3: Now 3 rows available — window is full
       AVG(100, 200, 150) = 150.00

Day 4: Window slides forward — drops Day 1
       AVG(200, 150, 300) = 216.67

Day 5: Window slides forward — drops Day 2
       AVG(150, 300, 250) = 233.33

Day 6: Window slides forward — drops Day 3
       AVG(300, 250, 400) = 316.67
```

**Visual of Sliding Window:**

```
Day  Sales    Window included           Moving Avg
 1    100     [100]                      100.00
 2    200     [100, 200]                 150.00
 3    150     [100, 200, 150]            150.00
 4    300     [200, 150, 300]  ← slid    216.67
 5    250     [150, 300, 250]  ← slid    233.33
 6    400     [300, 250, 400]  ← slid    316.67
 7    350     [250, 400, 350]  ← slid    333.33
 8    500     [400, 350, 500]  ← slid    416.67
 9    450     [350, 500, 450]  ← slid    433.33
10    600     [500, 450, 600]  ← slid    516.67
```

**Result:**

| DayNumber | SaleAmount | MovingAvg3Days |
| --------- | ---------- | -------------- |
| 1         | 100        | 100.00         |
| 2         | 200        | 150.00         |
| 3         | 150        | 150.00         |
| 4         | 300        | 216.67         |
| 5         | 250        | 233.33         |
| 6         | 400        | 316.67         |
| 7         | 350        | 333.33         |
| 8         | 500        | 416.67         |
| 9         | 450        | 433.33         |
| 10        | 600        | 516.67         |

### 2. Moving SUM&#x20;

Running total keeps **adding up values** as you go row by row like a balance that keeps growing.

Think of it like a **bank passbook** ,every transaction is added to the previous balance:

```
Day 1 — Deposit ₹100  → Balance: ₹100
Day 2 — Deposit ₹200  → Balance: ₹300
Day 3 — Deposit ₹150  → Balance: ₹450
Day 4 — Deposit ₹300  → Balance: ₹750
...and so on
```

**Example :** **Running Total of Sales:**

```sql
SELECT DayNumber,
       SaleAmount,
       SUM(SaleAmount)
       OVER (
           ORDER BY DayNumber
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS RunningTotal
FROM DailySales;
```

**How it calculates:**

```
Day 1: 100                    = 100
Day 2: 100 + 200              = 300
Day 3: 100 + 200 + 150        = 450
Day 4: 100 + 200 + 150 + 300  = 750
Day 5: 750 + 250              = 1000
...keeps adding
```

**Visual -> Running Total:**

```
Day  Sales    All rows included so far        Running Total
 1    100     [100]                            100
 2    200     [100+200]                        300
 3    150     [100+200+150]                    450
 4    300     [100+200+150+300]                750
 5    250     [100+200+150+300+250]            1000
 6    400     [...+400]                        1400
 7    350     [...+350]                        1750
 8    500     [...+500]                        2250
 9    450     [...+450]                        2700
10    600     [...+600]                        3300
```

**Result:**

| DayNumber | SaleAmount | RunningTotal |
| --------- | ---------- | ------------ |
| 1         | 100        | 100          |
| 2         | 200        | 300          |
| 3         | 150        | 450          |
| 4         | 300        | 750          |
| 5         | 250        | 1000         |
| 6         | 400        | 1400         |
| 7         | 350        | 1750         |
| 8         | 500        | 2250         |
| 9         | 450        | 2700         |
| 10        | 600        | 3300         |

## CTE (Common Table Expression)

#### What is a CTE?

A CTE is a **temporary named result set** ,you write a query, give it a name, and then use that name in your main query just like a temporary table that exists only for that query.

Think of it like a **rough work space** in an exam , you do your calculations on the side, name them, and use those results in your final answer. After the exam it disappears.

**Visual Diagram of How CTE Works:**

```
Step 1 — CTE runs first and creates temp result:
┌─────────────────────────────────┐
│  WITH DeptAvg AS (              │
│  SELECT Department,             │
│  AVG(Salary) AS AvgSalary       │
│  FROM Employee                  │
│  GROUP BY Department)           │
│                                 │
│  Result stored as "DeptAvg":    │
│  ┌────────────┬──────────┐      │
│  │ Department │AvgSalary │      │
│  │ IT         │ 50500    │      │
│  │ HR         │ 52666    │      │
│  │ Finance    │ 63333    │      │
│  └────────────┴──────────┘      │
└─────────────────────────────────┘
         ↓
Step 2 — Main query uses CTE result:
┌─────────────────────────────────┐
│  SELECT E.FullName,             │
│  E.Salary, D.AvgSalary          │
│  FROM Employee E                │
│  JOIN DeptAvg D                 │
│  WHERE E.Salary > D.AvgSalary   │
└─────────────────────────────────┘
         ↓
Final Result shown to user
```

#### Syntax:

```sql
WITH CTEName AS (
    -- your SELECT query here
    SELECT columns
    FROM table
    WHERE condition
)
-- main query using the CTE
SELECT * FROM CTEName;
```

#### Example 1 :  Find employees earning above department average:

```sql
WITH DeptAvg AS (
    SELECT Department,
           AVG(Salary) AS AvgSalary
    FROM Employee
    GROUP BY Department
)
SELECT E.FullName,
       E.Department,
       E.Salary,
       D.AvgSalary AS DeptAverage
FROM Employee E
JOIN DeptAvg D ON E.Department = D.Department
WHERE E.Salary > D.AvgSalary;
```

**Result:**

| FullName    | Department | Salary | DeptAverage |
| ----------- | ---------- | ------ | ----------- |
| Neha Singh  | Finance    | 70000  | 63333       |
| Kavya Reddy | HR         | 65000  | 52666       |
| Sneha Patil | IT         | 55000  | 50500       |
| Pooja Nair  | IT         | 55000  | 50500       |
