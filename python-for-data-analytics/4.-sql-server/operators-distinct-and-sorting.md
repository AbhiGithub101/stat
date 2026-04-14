---
hidden: true
---

# Operators, Distinct & Sorting

> Our Reference Table -> **matches**

```sql
SELECT * FROM matches;
```

| id  | season | city      | date     | team1               | team2                       | toss\_winner                | toss\_decision | result | dl\_applied | winner                 | win\_by\_runs | win\_by\_wickets | player\_of\_match | venue                                   | umpire1        | umpire2   | umpire3 |
| --- | ------ | --------- | -------- | ------------------- | --------------------------- | --------------------------- | -------------- | ------ | ----------- | ---------------------- | ------------- | ---------------- | ----------------- | --------------------------------------- | -------------- | --------- | ------- |
| 1   | 2017   | Hyderabad | 4/5/2017 | Sunrisers Hyderabad | Royal Challengers Bangalore | Royal Challengers Bangalore | field          | normal | 0           | Sunrisers Hyderabad    | 35            | 0                | Yuvraj Singh      | Rajiv Gandhi International Stadium      | AY Dandekar    | NJ Llong  |         |
| 2   | 2017   | Pune      | 4/6/2017 | Mumbai Indians      | Rising Pune Supergiant      | Rising Pune Supergiant      | field          | normal | 0           | Rising Pune Supergiant | 0             | 7                | SPD Smith         | Maharashtra Cricket Association Stadium | A Nand Kishore | S Ravi    |         |
| 3   | 2017   | Rajkot    | 4/7/2017 | Gujarat Lions       | Kolkata Knight Riders       | Kolkata Knight Riders       | field          | normal | 0           | Kolkata Knight Riders  | 0             | 10               | CA Lynn           | Saurashtra Cricket Association Stadium  | Nitin Menon    | CK Nandan |         |
| ... | ...    | ...       | ...      | ...                 | ...                         | ...                         | ...            | ...    | ...         | ...                    | ...           | ...              | ...               | ...                                     | ...            | ...       | ...     |

## What is the WHERE Clause?

WHERE is used to **filter rows** from a table — it tells SQL _"only show me rows that match this condition."_

Without WHERE , you get everything:

```sql
SELECT * FROM matches;
-- Returns all 756 rows
```

With WHERE ,you get only what you need:

```sql
SELECT * FROM matches
WHERE city = 'Hyderabad';
-- Returns only matches played in Hyderabad
```

Think of it like a **search filter** on Swiggy or Amazon instead of seeing all products, you filter by city, price, or category. WHERE does exactly that for your table.

<img src="../../.gitbook/assets/file.excalidraw (7).svg" alt="" class="gitbook-drawing">

## Operators Used with WHERE

### 1. = (Equal To)

Finds rows where the value is **exactly equal** to what you specify.

sql

```sql
SELECT * FROM matches
WHERE city = 'Mumbai';
```

**Result — only Mumbai matches:**

| id | season | city   | winner         | player\_of\_match |
| -- | ------ | ------ | -------------- | ----------------- |
| 7  | 2017   | Mumbai | Mumbai Indians | N Rana            |
| 10 | 2017   | Mumbai | Mumbai Indians | JJ Bumrah         |
| 16 | 2017   | Mumbai | Mumbai Indians | N Rana            |

### 2. != and <> (Not Equal To)

Both `!=` and `<>` mean the same thing — **not equal to.** They give you all rows that do NOT match the value.

```sql
SELECT * FROM matches
WHERE city != 'Mumbai';
```

or

```sql
SELECT * FROM matches
WHERE city <> 'Mumbai';
```

**Result — every match except Mumbai:**

| id  | season | city      | winner                 |
| --- | ------ | --------- | ---------------------- |
| 1   | 2017   | Hyderabad | Sunrisers Hyderabad    |
| 2   | 2017   | Pune      | Rising Pune Supergiant |
| 3   | 2017   | Rajkot    | Kolkata Knight Riders  |
| ... | ...    | ...       | ...                    |

> Both `!=` and `<>` do the exact same job. `!=` is more commonly used. `<>` is the older SQL standard way.

### 3. > (Greater Than)

Finds rows where the value is **more than** what you specify.sql

```sql
SELECT * FROM matches
WHERE win_by_runs > 50;
```

**Result — matches won by more than 50 runs:**

| id | city  | winner           | win\_by\_runs |
| -- | ----- | ---------------- | ------------- |
| 9  | Pune  | Delhi Daredevils | 97            |
| 15 | Delhi | Delhi Daredevils | 51            |

### 4. < (Less Than)

Finds rows where the value is **less than** what you specify.

```sql
SELECT * FROM matches
WHERE win_by_wickets < 5;
```

**Result — matches won by less than 5 wickets:**

| id | city   | winner                | win\_by\_wickets |
| -- | ------ | --------------------- | ---------------- |
| 7  | Mumbai | Mumbai Indians        | 4                |
| 10 | Mumbai | Mumbai Indians        | 4                |
| 18 | Delhi  | Kolkata Knight Riders | 4                |

### 5. >= (Greater Than or Equal To)

Finds rows where the value is **more than or exactly equal** to what you specify.

```sql
SELECT * FROM matches
WHERE win_by_runs >= 35;
```

**Result — matches won by 35 runs or more:**

| id | city      | winner              | win\_by\_runs |
| -- | --------- | ------------------- | ------------- |
| 1  | Hyderabad | Sunrisers Hyderabad | 35            |
| 9  | Pune      | Delhi Daredevils    | 97            |
| 15 | Delhi     | Delhi Daredevils    | 51            |

### 6. <= (Less Than or Equal To)

Finds rows where the value is **less than or exactly equal** to what you specify.

sql

```sql
SELECT * FROM matches
WHERE win_by_wickets <= 4;
```

**Result — matches won by 4 wickets or fewer:**

| id | city   | winner                | win\_by\_wickets |
| -- | ------ | --------------------- | ---------------- |
| 7  | Mumbai | Mumbai Indians        | 4                |
| 10 | Mumbai | Mumbai Indians        | 4                |
| 18 | Delhi  | Kolkata Knight Riders | 4                |

### 7. LIKE (Pattern Matching)

LIKE is used when you want to **search for a pattern inside text** ,not an exact match.

It uses two special symbols:

| Symbol | Meaning                  | Example                                  |
| ------ | ------------------------ | ---------------------------------------- |
| `%`    | Any number of characters | `'M%'` means starts with M               |
| `_`    | Exactly one character    | `'_avi'` means any one letter then "avi" |

#### LIKE Examples:

**Find all players whose name starts with 'S':**

sql

```sql
SELECT * FROM matches
WHERE player_of_match LIKE 'S%';
```

| id | player\_of\_match | winner                 |
| -- | ----------------- | ---------------------- |
| 2  | SPD Smith         | Rising Pune Supergiant |
| 9  | SV Samson         | Delhi Daredevils       |

**Find all cities that end with 'e':**

```sql
SELECT * FROM matches
WHERE city LIKE '%e';
```

| id | city   | winner                 |
| -- | ------ | ---------------------- |
| 2  | Pune   | Rising Pune Supergiant |
| 4  | Indore | KIngs XI Punjab        |

**Find all venues that contain the word 'Stadium':**

```sql
SELECT * FROM matches
WHERE venue LIKE '%Stadium%';
```

> Returns every match played at any venue that has the word "Stadium" in its name.

### 8. NOT LIKE

Opposite of LIKE — gives you all rows that **do NOT match** the pattern.

```sql
SELECT * FROM matches
WHERE city NOT LIKE 'H%';
```

**Result — all matches NOT played in cities starting with H (so no Hyderabad):**

| id  | city   | winner                 |
| --- | ------ | ---------------------- |
| 2   | Pune   | Rising Pune Supergiant |
| 3   | Rajkot | Kolkata Knight Riders  |
| 4   | Indore | Kings XI Punjab        |
| ... | ...    | ...                    |

### Quick Recap — All Operators

| Operator     | Meaning                | Example                     |
| ------------ | ---------------------- | --------------------------- |
| `=`          | Exactly equal          | `city = 'Mumbai'`           |
| `!=` or `<>` | Not equal              | `city != 'Mumbai'`          |
| `>`          | Greater than           | `win_by_runs > 50`          |
| `<`          | Less than              | `win_by_wickets < 5`        |
| `>=`         | Greater than or equal  | `win_by_runs >= 35`         |
| `<=`         | Less than or equal     | `win_by_wickets <= 4`       |
| `LIKE`       | Matches a pattern      | `player_of_match LIKE 'S%'` |
| `NOT LIKE`   | Does not match pattern | `city NOT LIKE 'H%'`        |





