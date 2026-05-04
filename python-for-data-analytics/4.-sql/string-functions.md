# String Functions

> Our Reference Table : deliveries

#### What are String Functions?

String functions are **built-in SQL functions** that help you work with text data  like cutting a part of a name, converting to uppercase, removing extra spaces, finding a character inside text, and more.

#### 1. LEN()

LEN returns the **total number of characters** in a text value including spaces in between but **not trailing spaces at the end.**

**Syntax:**

```sql
SELECT LEN(column_name) FROM table_name;
```

**Example 1 :**

```sql
SELECT LEN('DA Warner') AS Length;
-- Output: 9
```

**Example 2 : find the length of each batsman's name:**

```sql
SELECT DISTINCT batsman, LEN(batsman) AS NameLength
FROM deliveries;
```

#### 2. DATALENGTH()

DATALENGTH returns the **number of bytes** used to store the value not just characters.

**Syntax:**

```sql
SELECT DATALENGTH(column_name) FROM table_name;
```

**Example:**

```sql
SELECT DISTINCT batsman,
       LEN(batsman)        AS LenResult,
       DATALENGTH(batsman) AS DataLengthResult
FROM deliveries;
```

**Result:**

| batsman   | LenResult | DataLengthResult |
| --------- | --------- | ---------------- |
| MK Pandey | 9         | 18               |
| R Dravid  | 8         | 16               |

**LEN vs DATALENGTH : What is the difference?**

|                 | LEN()        | DATALENGTH()                      |
| --------------- | ------------ | --------------------------------- |
| What it counts  | Characters   | Bytes                             |
| Trailing spaces | Ignores them | Counts them                       |
| For VARCHAR     | Same result  | Same result                       |
| For NVARCHAR    | Same result  | 2x result (2 bytes per character) |

**Example showing the difference with NVARCHAR:**

```sql
SELECT LEN(N'DA Warner')        AS LenResult;        -- Output: 9
SELECT DATALENGTH(N'DA Warner') AS DataLengthResult;  -- Output: 18
```

> NVARCHAR stores 2 bytes per character so 9 characters = 18 bytes. LEN still shows 9 because it counts characters not bytes.

**Example showing trailing spaces:**

```sql
SELECT LEN('DA Warner   ')        AS LenResult;        -- Output: 9  (ignores spaces)
SELECT DATALENGTH('DA Warner   ') AS DataLengthResult;  -- Output: 12 (counts spaces)
```

#### 3. UPPER()

UPPER converts all text to **CAPITAL LETTERS.**

**Syntax:**

```sql
SELECT UPPER(column_name) FROM table_name;
```

**Example 1 :**

```sql
SELECT UPPER('DA Warner') AS uppercase;
-- Output: DA WARNER
```

**Example 2:  show all batsman names in uppercase:**

```sql
SELECT DISTINCT batsman, UPPER(batsman) AS UpperName
FROM deliveries;
```

#### 4. LOWER()

LOWER converts all text to **small letters.**

**Syntax:**

```sql
SELECT LOWER(column_name) FROM table_name;
```

**Example: show all bowler names in lowercase:**

```sql
SELECT DISTINCT bowler, LOWER(bowler) AS LowerName
FROM deliveries;
```

#### 5. TRIM()

TRIM removes **extra spaces from both sides**( left and right ) of a text value.

**Syntax:**

```sql
SELECT TRIM(column_name) FROM table_name;
```

**Example:**

```sql
SELECT TRIM('   DA Warner   ') AS TrimResult;
-- Output: 'DA Warner'
```

> Spaces on both sides removed. Spaces in between are kept.

**Real-life use:** When data is imported from Excel or CSV, extra spaces often sneak in at the beginning or end of values. TRIM cleans them up.

#### 6. LTRIM()

LTRIM removes extra spaces from the **Left side only.**

**Syntax:**

```sql
SELECT LTRIM(column_name) FROM table_name;
```

**Example:**

```sql
SELECT LTRIM('   DA Warner   ') AS LTrimResult;
-- Output: 'DA Warner   '
```

> Left spaces removed. Right spaces still there.

#### 7. RTRIM()

RTRIM removes extra spaces from the **Right side only.**

**Syntax:**

```sql
SELECT RTRIM(column_name) FROM table_name;
```

**Example:**

```sql
SELECT RTRIM('   DA Warner   ') AS RTrimResult;
-- Output: '   DA Warner'
```

> Right spaces removed. Left spaces still there.

**TRIM vs LTRIM vs RTRIM -> Quick Comparison**

| Input           | Function | Output         |
| --------------- | -------- | -------------- |
| `' DA Warner '` | `TRIM`   | `'DA Warner'`  |
| `' DA Warner '` | `LTRIM`  | `'DA Warner '` |
| `' DA Warner '` | `RTRIM`  | `' DA Warner'` |

> &#x20;In most cases just use `TRIM` as it cleans both sides at once.

#### 8. SUBSTRING()

SUBSTRING extracts a **part of a text** , you tell it where to start and how many characters to pick.

**Syntax:**

```sql
SELECT SUBSTRING(column_name, start, length) FROM table_name;
```

* **start** → position to start from (starts at 1, not 0)
* **length** → how many characters to pick

**Example: Get only the first 2 characters of batsman name:**

```sql
SELECT DISTINCT batsman, SUBSTRING(batsman, 1, 2) AS ShortName
FROM deliveries;
```

**Result:**

| batsman    | ShortName |
| ---------- | --------- |
| KK Nair    | KK        |
| N Rana     | N         |
| BAW Mendis | BA        |

**Another example : extract 'Warner' from 'DA Warner':**

```sql
SELECT SUBSTRING('DA Warner', 4, 6) AS Result;
-- Output: Warner
```

> Start at position 4 (W), pick 6 characters → W-a-r-n-e-r

#### 9. LEFT()

LEFT picks a specified number of characters from the **left side (beginning)** of the text.

**Syntax:**

```sql
SELECT LEFT(column_name, number_of_characters) FROM table_name;
```

**Example : get first 3 characters of bowling team name:**

```sql
SELECT DISTINCT bowling_team, LEFT(bowling_team, 3) AS ShortName
FROM deliveries;
```

**Result:**

| bowling\_team       | ShortName |
| ------------------- | --------- |
| Mumbai Indians      | Mum       |
| Chennai Super Kings | Che       |

**Simple test:**

```sql
SELECT LEFT('DA Warner', 2) AS Result;
-- Output: DA
```

#### 10. RIGHT()

RIGHT picks a specified number of characters from the **right side (end)** of the text.

**Syntax:**

```sql
SELECT RIGHT(column_name, number_of_characters) FROM table_name;
```

**Example : get last 3 characters of batting team name:**

```sql
SELECT DISTINCT batting_team, RIGHT(batting_team, 3) AS LastChars
FROM deliveries;
```

**Result:**

| batting\_team           | LastChars |
| ----------------------- | --------- |
| Chennai Super Kings     | ngs       |
| Rising Pune Supergiants | nts       |

**Simple test:**

```sql
SELECT RIGHT('DA Warner', 6) AS Result;
-- Output: Warner
```

#### 11. CHARINDEX()

CHARINDEX finds the **position of a character or word** inside a text, it tells you at what position it appears.

**Syntax:**

```sql
SELECT CHARINDEX('search_text', column_name) FROM table_name;
```

**Example : find where the space appears in batsman name:**

```sql
SELECT DISTINCT batsman, CHARINDEX(' ', batsman) AS SpacePosition
FROM deliveries;
```

**Result:**

| batsman      | SpacePosition |
| ------------ | ------------- |
| F du Plessis | 2             |
| S Sohal      | 2             |
| Sunny Singh  | 6             |

**If the text is not found then CHARINDEX returns 0:**

```sql
SELECT CHARINDEX('z', 'DA Warner') AS Result;
-- Output: 0
```

#### 12. REVERSE()

REVERSE simply **reverses the entire text,**&#x6C;ast character becomes first.

**Syntax:**

```sql
SELECT REVERSE(column_name) FROM table_name;
```

**Example:**

```sql
SELECT DISTINCT batsman, REVERSE(batsman) AS ReversedName
FROM deliveries;
```

#### 13. REPLACE()

REPLACE finds a specific text inside a value and **replaces it with something else.**

**Syntax:**

```sql
SELECT REPLACE(column_name, 'old_text', 'new_text') FROM table_name;
```

**Example :** **replace 'Sunrisers Hyderabad' with 'SRH' in batting\_team:**

```sql
SELECT DISTINCT batting_team,
       REPLACE(batting_team, 'Sunrisers Hyderabad', 'SRH') AS ShortName
FROM deliveries;
```

#### 14. CONCAT()

CONCAT joins **two or more text values together** into one.

**Syntax:**

```sql
SELECT CONCAT(value1, value2, value3, ...) FROM table_name;
```

**Example : combine batsman and bowler names with ' vs ' in between:**

```sql
SELECT CONCAT(batsman, ' vs ', bowler) AS Matchup
FROM deliveries;
```
