# Operators, Distinct & Sorting

> Our Reference Table -> **matches**

```sql
SELECT * FROM matches;
```

| id  | season | city      | date       | team1               | team2                       | toss\_winner                | toss\_decision | result | dl\_applied | winner                 | win\_by\_runs | win\_by\_wickets | player\_of\_match | venue                                   | umpire1        | umpire2   | umpire3 |
| --- | ------ | --------- | ---------- | ------------------- | --------------------------- | --------------------------- | -------------- | ------ | ----------- | ---------------------- | ------------- | ---------------- | ----------------- | --------------------------------------- | -------------- | --------- | ------- |
| 1   | 2017   | Hyderabad | 2017-04-05 | Sunrisers Hyderabad | Royal Challengers Bangalore | Royal Challengers Bangalore | field          | normal | 0           | Sunrisers Hyderabad    | 35            | 0                | Yuvraj Singh      | Rajiv Gandhi International Stadium      | AY Dandekar    | NJ Llong  |         |
| 2   | 2017   | Pune      | 2017-04-06 | Mumbai Indians      | Rising Pune Supergiant      | Rising Pune Supergiant      | field          | normal | 0           | Rising Pune Supergiant | 0             | 7                | SPD Smith         | Maharashtra Cricket Association Stadium | A Nand Kishore | S Ravi    |         |
| 3   | 2017   | Rajkot    | 2017-04-07 | Gujarat Lions       | Kolkata Knight Riders       | Kolkata Knight Riders       | field          | normal | 0           | Kolkata Knight Riders  | 0             | 10               | CA Lynn           | Saurashtra Cricket Association Stadium  | Nitin Menon    | CK Nandan |         |
| ... | ...    | ...       | ...        | ...                 | ...                         | ...                         | ...            | ...    | ...         | ...                    | ...           | ...              | ...               | ...                                     | ...            | ...       | ...     |

## What is the WHERE clause?

WHERE is used to **filter rows** from a table,it tells SQL _"only show me rows that match this condition."_

Without WHERE ,you get everything:

```sql
SELECT * FROM matches;
-- Returns all 756 rows
```

With WHERE,you get only what you need:

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

```sql
SELECT * FROM matches
WHERE city = 'Mumbai';
```

**Result will include only Mumbai matches:**

| id | season | city   | winner         | player\_of\_match |
| -- | ------ | ------ | -------------- | ----------------- |
| 7  | 2017   | Mumbai | Mumbai Indians | N Rana            |
| 10 | 2017   | Mumbai | Mumbai Indians | JJ Bumrah         |
| 16 | 2017   | Mumbai | Mumbai Indians | N Rana            |

### 2. != and <> (Not Equal To)

Both `!=` and `<>` mean the same thing -> **not equal to.**&#x20;

They give you all rows that do NOT match the value.

```sql
SELECT * FROM matches
WHERE city != 'Mumbai';
```

or

```sql
SELECT * FROM matches
WHERE city <> 'Mumbai';
```

**Result will include every match except Mumbai:**

| id  | season | city      | winner                 |
| --- | ------ | --------- | ---------------------- |
| 1   | 2017   | Hyderabad | Sunrisers Hyderabad    |
| 2   | 2017   | Pune      | Rising Pune Supergiant |
| 3   | 2017   | Rajkot    | Kolkata Knight Riders  |
| ... | ...    | ...       | ...                    |

> Both `!=` and `<>` do the exact same job. `!=` is more commonly used. `<>` is the older SQL standard way.

### 3. > (Greater Than)

Finds rows where the value is **more than** what you specify.

```sql
SELECT * FROM matches
WHERE win_by_runs > 50;
```

**Result will include matches won by more than 50 runs:**

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

**Result will include matches won by 35 runs or more:**

| id | city      | winner              | win\_by\_runs |
| -- | --------- | ------------------- | ------------- |
| 1  | Hyderabad | Sunrisers Hyderabad | 35            |
| 9  | Pune      | Delhi Daredevils    | 97            |
| 15 | Delhi     | Delhi Daredevils    | 51            |

### 6. <= (Less Than or Equal To)

Finds rows where the value is **less than or exactly equal** to what you specify.

```sql
SELECT * FROM matches
WHERE win_by_wickets <= 4;
```

**Result will include matches won by 4 wickets or fewer:**

| id | city      | winner                      | win\_by\_wickets |
| -- | --------- | --------------------------- | ---------------- |
| 1  | Hyderabad | Sunrisers Hyderabad         | 0                |
| 5  | Bangalore | Royal Challengers Bangalore | 0                |
| 7  | Mumbai    | Mumbai Indians              | 4                |

### 7. LIKE (Pattern Matching)

LIKE is used when you want to **search for a pattern inside text** ,not an exact match.

It uses two special symbols:

| Symbol | Meaning                  | Example                                  |
| ------ | ------------------------ | ---------------------------------------- |
| `%`    | Any number of characters | `'M%'` means starts with M               |
| `_`    | Exactly one character    | `'_avi'` means any one letter then "avi" |

#### LIKE Examples:

**Find all players whose name starts with 'S':**

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

Opposite of LIKE gives you all rows that **do NOT match** the pattern.

```sql
SELECT * FROM matches
WHERE city NOT LIKE 'H%';
```

**Result will include all matches NOT played in cities starting with H (so no Hyderabad):**

| id  | city   | winner                 |
| --- | ------ | ---------------------- |
| 2   | Pune   | Rising Pune Supergiant |
| 3   | Rajkot | Kolkata Knight Riders  |
| 4   | Indore | Kings XI Punjab        |
| ... | ...    | ...                    |

### Quick Recap of All Operators

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

## DISTINCT Clause

Let us say you want to see all the cities where IPL matches were played:

```sql
SELECT city FROM matches;
```

**Result:**

| city      |
| --------- |
| Hyderabad |
| Pune      |
| Rajkot    |
| Indore    |
| Bangalore |
| Hyderabad |
| Mumbai    |
| Indore    |
| Pune      |
| Mumbai    |
| ...       |

**DISTINCT** removes all duplicates and shows you **only unique values.**

```sql
SELECT DISTINCT city FROM matches;
```

**Result will include each city appearing only once:**

| city      |
| --------- |
| Hyderabad |
| Pune      |
| Rajkot    |
| Indore    |
| Bangalore |
| Mumbai    |
| Kolkata   |
| Delhi     |
| Rajkot    |

> Think of it like a attendance register , DISTINCT makes sure each name appears only once no matter how many times it was repeated.

#### DISTINCT Examples

**All unique teams that won a match:**

```sql
SELECT DISTINCT winner FROM matches;
```

**All unique players who won Player of the Match:**

```sql
SELECT DISTINCT player_of_match FROM matches;
```

**All unique toss decisions made:**

```sql
SELECT DISTINCT toss_decision FROM matches;
-- Result: bat, field
```

## Sorting :  ORDER BY

### What is Sorting?

Sorting means **arranging your results in a specific order** ,either from smallest to largest or largest to smallest.

Think of it like arranging students by their marks,either lowest to highest or highest to lowest. ORDER BY does the same for your query results.

**Syntax:**

```sql
SELECT * FROM matches
ORDER BY ColumnName ASC;   -- Ascending (small to large)

SELECT * FROM matches
ORDER BY ColumnName DESC;  -- Descending (large to small)
```

### ASC - Ascending Order (Default)

Arranges data from **smallest to largest** -> numbers go 1,2,3 and text goes A,B,C.

```sql
SELECT id, city, winner, win_by_runs FROM matches
ORDER BY win_by_runs ASC;
```

**Result will include matches sorted from lowest win margin to highest:**

| id  | city      | winner                      | win\_by\_runs |
| --- | --------- | --------------------------- | ------------- |
| 2   | Pune      | Rising Pune Supergiant      | 0             |
| 3   | Rajkot    | Kolkata Knight Riders       | 0             |
| 4   | Indore    | Kings XI Punjab             | 0             |
| ... | ...       | ...                         | ...           |
| 6   | Bangalore | Royal Challengers Bangalore | 144           |
| 44  | Delhi     | Mumbai Indians              | 146           |

> ASC is actually the **default** , if you write just `ORDER BY win_by_runs` without ASC or DESC, SQL will sort ascending automatically.

### DESC - Descending Order

Arranges data from **largest to smallest** -> numbers go 9,8,7 and text goes Z,Y,X.

```sql
SELECT id, city, winner, win_by_runs FROM matches
ORDER BY win_by_runs DESC;
```

**Result will include matches sorted from highest win margin to lowest:**

| id  | city      | winner                      | win\_by\_runs |
| --- | --------- | --------------------------- | ------------- |
| 9   | Pune      | Delhi Daredevils            | 97            |
| 15  | Delhi     | Delhi Daredevils            | 51            |
| 1   | Hyderabad | Sunrisers Hyderabad         | 35            |
| 20  | Rajkot    | Royal Challengers Bangalore | 21            |
| ... | ...       | ...                         | ...           |

### Sorting Text Columns

Sorting also works on **text columns**&#x20;

it sorts **alphabetically**:

```sql
SELECT DISTINCT city FROM matches
ORDER BY city ASC;
```

**Result will include cities in alphabetical order:**

| city      |
| --------- |
| Bangalore |
| Delhi     |
| Hyderabad |
| Indore    |
| Kolkata   |
| Mumbai    |
| Pune      |
| Rajkot    |

### Combining WHERE + ORDER BY

You can filter and sort at the same time:

```sql
SELECT id, city, winner, win_by_runs FROM matches
WHERE toss_decision = 'bat'
ORDER BY win_by_runs DESC;
```

> This gives you only matches where the toss winner chose to bat,sorted by highest win margin first.
