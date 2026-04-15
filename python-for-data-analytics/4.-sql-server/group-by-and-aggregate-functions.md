---
hidden: true
---

# Group By and Aggregate Functions

> Our Reference Table -> **matches**

## 1. Ordinal Sorting

We already covered `ORDER BY` using column names in the last module. Ordinal sorting is just a **shorter way** of doing the same thing instead of writing the column name, you write its **position number** in the SELECT statement.

**Normal way -> using column name:**

```sql
SELECT * FROM matches
ORDER BY city DESC;
```

**Ordinal way -> using column position number:**

```sql
SELECT * FROM matches
ORDER BY 3 DESC;


```

> Both queries give **exactly the same result.** In the second one, `3` means the 3rd column in the matches table  which is `city`.

#### How to count the position:

```sql
SELECT * FROM matches
--      1    2       3     4     5      6         7            8              9       10          11          12               13                14     15       16       17       18
--      id  season  city  date  team1  team2  toss_winner  toss_decision  result  dl_appli
```

| Position | Column            |
| -------- | ----------------- |
| 1        | id                |
| 2        | season            |
| 3        | city              |
| 4        | date              |
| 5        | team1             |
| 6        | team2             |
| 7        | toss\_winner      |
| 8        | toss\_decision    |
| 9        | result            |
| 10       | dl\_applied       |
| 11       | winner            |
| 12       | win\_by\_runs     |
| 13       | win\_by\_wickets  |
| 14       | player\_of\_match |
| 15       | venue             |
| 16       | umpire1           |
| 17       | umpire2           |
| 18       | umpire3           |

#### Example 1 -> Sort by city A to Z (ASC)

```sql
SELECT * FROM matches
ORDER BY 3 ASC;
```

**Result -> sorted by city alphabetically:**

| id  | season | city      | winner                      | ... |
| --- | ------ | --------- | --------------------------- | --- |
| 5   | 2017   | Bangalore | Royal Challengers Bangalore | ... |
| 12  | 2017   | Bangalore | Mumbai Indians              | ... |
| 17  | 2017   | Bangalore | Rising Pune Supergiant      | ... |
| 15  | 2017   | Delhi     | Delhi Daredevils            | ... |
| 18  | 2017   | Delhi     | Kolkata Knight Riders       | ... |
| ... | ...    | ...       | ...                         | ... |

***

Example 2 -> Sort by win\_by\_runs highest first (DESC)

```sql
SELECT * FROM matches
ORDER BY 12 DESC;
```

**Result -> matches with highest win margin by runs first:**

| id  | season | city      | winner                 | win\_by\_runs |
| --- | ------ | --------- | ---------------------- | ------------- |
| 9   | 2017   | Pune      | Delhi Daredevils       | 97            |
| 15  | 2017   | Delhi     | Delhi Daredevils       | 51            |
| 1   | 2017   | Hyderabad | Sunrisers Hyderabad    | 35            |
| 17  | 2017   | Bangalore | Rising Pune Supergiant | 27            |
| ... | ...    | ...       | ...                    | ...           |

#### Another Example:

```sql
SELECT id, city, winner, win_by_runs FROM matches
ORDER BY 2 ASC;
```

> This sorts by position 2 which is `city` — alphabetically A to Z.

| id  | city      | winner                      | win\_by\_runs |
| --- | --------- | --------------------------- | ------------- |
| 5   | Bangalore | Royal Challengers Bangalore | 15            |
| 17  | Bangalore | Rising Pune Supergiant      | 27            |
| 15  | Delhi     | Delhi Daredevils            | 51            |
| 18  | Delhi     | Kolkata Knight Riders       | 0             |
| ... | ...       | ...                         | ...           |

## 2. GROUP BY

### The Problem First

Let us say you want to know **how many matches were played in each city.**

If you just run:

```sql
SELECT city FROM matches;
```

You get a long list of cities repeating again and again , not useful at all.

What you actually want is:

| city      | total matches |
| --------- | ------------- |
| Mumbai    | 5             |
| Hyderabad | 3             |
| Pune      | 3             |
| ...       | ...           |

This is exactly what **GROUP BY** does ,it **groups all rows that have the same value** in a column and lets you perform calculations on each group.

Think of it like this: You have a box of cricket cards  and you want to sort them by team -> all Mumbai Indians together, all CSK together, all RCB together. GROUP BY does that sorting and grouping for your data.

**Syntax:**

```sql
SELECT column, aggregate_function
FROM table
GROUP BY column;
```

#### Simple GROUP BY Example

**How many matches were played in each city?**

```sql
SELECT city, COUNT(*) AS TotalMatches
FROM matches
GROUP BY city;
```

**Result:**

| city         | TotalMatches |
| ------------ | ------------ |
| Abu Dhabi    | 7            |
| Ahmedabad    | 12           |
| Bangalore    | 66           |
| Bloemfontein | 2            |
| Cape Town    | 7            |
| ...          | ...          |

> Don't worry about COUNT(\*) yet — we will explain it properly in the next section. Just understand that GROUP BY is what created the groups here.

#### Important Rule about GROUP BY

> Every column you write in SELECT **must either be in GROUP BY or inside an aggregate function.** You cannot SELECT a column that is not grouped.

```sql
-- ✅ Correct
SELECT city, COUNT(*) FROM matches GROUP BY city;

-- ❌ Wrong — winner is not in GROUP BY or aggregate function
SELECT city, winner, COUNT(*) FROM matches GROUP BY city;
```

### 3. Aggregate Functions

Aggregate functions perform a **calculation on a group of rows** and return a single result. They are always used with GROUP BY or alone when you want the result for the whole table.

#### A) COUNT — Count the number of rows

COUNT counts **how many rows** exist — either in the whole table or in each group.

**Count total matches in the whole table:**

```sql
SELECT COUNT(*) AS TotalMatches
FROM matches;
```

| TotalMatches |
| ------------ |
| 636          |

**Count matches won by each team:**

```sql
SELECT winner, COUNT(*) AS MatchesWon
FROM matches
GROUP BY winner;
```

**Result:**

| winner               | MatchesWon |
| -------------------- | ---------- |
| Chennai Super Kings  | 79         |
| Deccan Chargers      | 29         |
| Delhi Daredevils     | 62         |
| Gujarat Lions        | 13         |
| Kings XI Punjab      | 70         |
| Kochi Tuskers Kerala | 6          |
| Mumbai Indians       | 77         |
| ...                  | ...        |

#### B) SUM — Add up values

SUM adds up all the values in a numeric column.

**Total runs scored across all matches by win margin:**

```sql
SELECT SUM(win_by_runs) AS TotalRunsMargin
FROM matches;
```

| TotalRunsMargin |
| --------------- |
| 8702            |

**Result:**

| winner              | TotalWinByRuns |
| ------------------- | -------------- |
| Chennai Super Kings | 1587           |
| Deccan Chargers     | 421            |
| Delhi Daredevils    | 571            |
| Gujarat Lions       | 1              |
| Kings XI Punjab     | 862            |
| ...                 | ...            |

#### C) AVG — Average of values

AVG calculates the **average** of a numeric column.

**Average win margin by runs across all matches:**

```sql
SELECT AVG(win_by_runs) AS AvgWinByRuns
FROM matches;
```

| AvgWinByRuns |
| ------------ |
| 13           |

**Average win by runs for each team:**

```sql
SELECT winner, AVG(win_by_runs) AS AvgWinByRuns
FROM matches
GROUP BY winner;
```

**Result:**

| winner              | AvgWinByRuns |
| ------------------- | ------------ |
| Chennai Super Kings | 20           |
| Deccan Chargers     | 14           |
| Delhi Daredevils    | 9            |
| Delhi Daredevil     | 0            |
| ...                 | ...          |

#### D) MIN -> Smallest value

MIN finds the **lowest value** in a column.

**Lowest win by runs in any match:**

```sql
SELECT MIN(win_by_runs) AS LowestWinByRuns
FROM matches;
```

| LowestWinByRuns |
| --------------- |
| 0               |

**Lowest win by runs for each team:**

```sql
SELECT winner, MIN(win_by_runs) AS LowestWinByRuns
FROM matches
GROUP BY winner;
```

#### E) MAX -> Largest value

MAX finds the **highest value** in a column.

**Highest win by runs in any match:**

```sql
SELECT MAX(win_by_runs) AS HighestWinByRuns
FROM matches;
```

| HighestWinByRuns |
| ---------------- |
| 146              |

**Highest win by runs for each team:**

```sql
SELECT winner, MAX(win_by_runs) AS HighestWinByRuns
FROM matches
GROUP BY winner;
```

**Result:**

| winner              | HighestWinByRuns |
| ------------------- | ---------------- |
| Chennai Super Kings | 97               |
| Deccan Chargers     | 82               |
| Delhi Daredevils    | 97               |
| Gujarat Lions       | 1                |
| Kings XI Punjab     | 111              |

#### Let's summarize all Aggregate Functions

| Function      | What it does         | Example                  |
| ------------- | -------------------- | ------------------------ |
| `COUNT(*)`    | Counts total rows    | Total matches played     |
| `SUM(column)` | Adds up all values   | Total runs in win margin |
| `AVG(column)` | Calculates average   | Average win margin       |
| `MIN(column)` | Finds smallest value | Lowest win margin        |
| `MAX(column)` | Finds largest value  | Highest win margin       |
