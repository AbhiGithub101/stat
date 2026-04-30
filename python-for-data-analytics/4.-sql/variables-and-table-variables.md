---
hidden: true
---

# Variables & Table Variables

## What is a Variable?

A variable is a **temporary storage box** in SQL , you can put a value in it, use it in your queries, and it disappears when your session ends.

Think of it like a sticky note , you write something on it, use it while you need it, and throw it away when done.

### 1. Declaring a Variable

To create a variable in SQL Server you use the `DECLARE` keyword.

**Syntax:**

```sql
DECLARE @VariableName DataType;
```

> All variables in SQL Server start with **@** sign.

**Examples:**

```sql
DECLARE @PlayerName  VARCHAR(100);
DECLARE @MatchCount  INT;
DECLARE @TodayDate   DATE;
DECLARE @RunsScored  DECIMAL(10,2);
```

> Just declaring a variable does not give it a value , it is empty (NULL) at this point.

### 2. Assigning / Storing Data in a Variable

After declaring, you store a value using **SET** or **SELECT.**

**Using SET:**

```sql
DECLARE @PlayerName VARCHAR(100);
SET @PlayerName = 'Virat Kohli';

SELECT @PlayerName AS PlayerName;
-- Output: Virat Kohli
```

**Using SELECT:**

```sql
DECLARE @MatchCount INT;
SELECT @MatchCount = 20;

SELECT @MatchCount AS TotalMatches;
-- Output: 20
```

### 3. Storing a Column's Data Value in a Variable

You can store the result of a query directly into a variable:

```sql
DECLARE @FirstWinner VARCHAR(100);
SELECT @FirstWinner = winner FROM matches WHERE id = 1;

SELECT @FirstWinner AS FirstMatchWinner;
-- Output: Sunrisers Hyderabad
```

```sql
DECLARE @MaxRuns INT;
DECLARE @MinRuns INT;
SELECT @MaxRuns = MAX(win_by_runs),
       @MinRuns = MIN(win_by_runs)
FROM matches;

SELECT @MaxRuns AS HighestWin, @MinRuns AS LowestWin;
-- Output: HighestWin = 97, LowestWin = 0
```

> Using SELECT you can assign multiple variables in one go.

### 4. Table Variable

A Table Variable is a **special variable that holds an entire table** not just one value. It is like a temporary table that lives only for the duration of your query or batch.

Think of it like a **temporary notepad** that holds multiple rows and columns and you can INSERT, SELECT and even JOIN with it.

**Syntax:**

```sql
DECLARE @VariableName TABLE (
    Column1 DataType,
    Column2 DataType,
    ...
);
```

**Example -> Create and use a Table Variable:**

```sql
-- Declare a table variable
DECLARE @TopWinners TABLE (
    TeamName    VARCHAR(100),
    MatchesWon  INT
);

-- Insert data into it
INSERT INTO @TopWinners (TeamName, MatchesWon)
SELECT winner, COUNT(*) AS MatchesWon
FROM matches
GROUP BY winner
HAVING COUNT(*) > 2;

-- Select from it like a normal table
SELECT * FROM @TopWinners;
```

**Result:**

| TeamName              | MatchesWon |
| --------------------- | ---------- |
| Sunrisers Hyderabad   | 3          |
| Kolkata Knight Riders | 3          |
| Mumbai Indians        | 4          |
| Delhi Daredevils      | 3          |

> **Coming Up Next:** Imagine you have a very long and complex query that you use every day, wouldn't it be great to just save it and call it with one word? That is a **View.** And imagine SQL automatically sending an alert or updating another table the moment someone deletes a record ,that is a **Trigger.** Both coming up in the next module!
