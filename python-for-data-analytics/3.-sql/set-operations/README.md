# Set Operations

## What are Set Operations?

Set Operations are used to **combine results of two or more SELECT queries** into one result without using joins.

Think of it like combining two lists :

* You have a list of players who scored in match 1
* You have a list of players who scored in match 2
* Set operations let you combine, compare or find differences between these two lists

> &#x20;**One important rule**  -> for set operations to work, both SELECT queries must have:
>
> * **Same number of columns**
> * **Compatible data types** in each column position

> Our Reference Table -> matches

We will use these two simple queries as our "two sets" throughout all examples:

#### Set A -> Matches won by batting first (toss decision = bat):

```sql
SELECT winner FROM matches WHERE toss_decision = 'bat';
```

| winner                      |
| --------------------------- |
| Royal Challengers Bangalore |
| Delhi Daredevils            |
| Delhi Daredevils            |
| Royal Challengers Bangalore |
| Delhi Daredevils            |

#### **Set B -> Matches won by fielding first (toss decision = field):**

```sql
SELECT winner FROM matches WHERE toss_decision = 'field';
```

| winner                      |
| --------------------------- |
| Sunrisers Hyderabad         |
| Rising Pune Supergiant      |
| Kolkata Knight Riders       |
| Kings XI Punjab             |
| Mumbai Indians              |
| Mumbai Indians              |
| Kolkata Knight Riders       |
| Mumbai Indians              |
| Sunrisers Hyderabad         |
| Mumbai Indians              |
| Kolkata Knight Riders       |
| Mumbai Indians              |
| Gujarat Lions               |
| Sunrisers Hyderabad         |
| Royal Challengers Bangalore |

### 1. UNION

UNION combines results of two queries into **one list** and **removes all duplicates** ,each value appears only once.

**Visual Diagram:**

```
Set A                    Set B
┌──────────────────┐    ┌──────────────────┐
│ RCB              │    │ SRH              │
│ Delhi Daredevils │    │ Rising Pune      │
│ Delhi Daredevils │    │ KKR              │
│ RCB              │    │ Kings XI Punjab  │
│ Delhi Daredevils │    │ Mumbai Indians   │
└──────────────────┘    │ Mumbai Indians   │
                        │ RCB              │
                        └──────────────────┘

           UNION Result
     ┌──────────────────────┐
     │ RCB          ───────►│ (duplicates removed)
     │ Delhi Daredevils     │
     │ SRH                  │
     │ Rising Pune          │
     │ KKR                  │
     │ Kings XI Punjab      │
     │ Mumbai Indians       │
     │ Gujarat Lions        │
     └──────────────────────┘
```

**Venn Diagram:**

```
        Set A              Set B
      ┌────────┐         ┌────────┐
      │  RCB   │         │  SRH   │
      │ Delhi  │─────────│  KKR   │
      │        │  Both   │ Mumbai │
      └────────┘         └────────┘
            ↕
    UNION = Everything from
    both sets, no duplicates
```

***

**Syntax:**

```sql
SELECT column FROM TableA
UNION
SELECT column FROM TableB;
```

**Example:**

```sql
SELECT winner FROM matches WHERE toss_decision = 'bat'
UNION
SELECT winner FROM matches WHERE toss_decision = 'field';
```

**Result :** **every team that won, shown only once:**

| winner                      |
| --------------------------- |
| Royal Challengers Bangalore |
| Delhi Daredevils            |
| Sunrisers Hyderabad         |
| Rising Pune Supergiant      |
| Kolkata Knight Riders       |
| Kings XI Punjab             |
| Mumbai Indians              |
| Gujarat Lions               |

> Even though Delhi Daredevils appeared 3 times and Mumbai Indians appeared 5 times , UNION shows each team **only once.**

### 2. UNION ALL

UNION ALL combines results of two queries into **one list** but **keeps all duplicates** ,every row from both queries appears.

**Visual Diagram:**

```
Set A                    Set B
┌──────────────────┐    ┌──────────────────┐
│ RCB              │    │ SRH              │
│ Delhi Daredevils │    │ Rising Pune      │
│ Delhi Daredevils │    │ KKR              │
│ RCB              │    │ Kings XI Punjab  │
│ Delhi Daredevils │    │ Mumbai Indians   │
└──────────────────┘    │ Mumbai Indians   │
                        │ RCB              │
                        └──────────────────┘

         UNION ALL Result
     ┌──────────────────────┐
     │ RCB                  │ ← from Set A
     │ Delhi Daredevils     │ ← from Set A
     │ Delhi Daredevils     │ ← from Set A (kept!)
     │ RCB                  │ ← from Set A (kept!)
     │ Delhi Daredevils     │ ← from Set A (kept!)
     │ SRH                  │ ← from Set B
     │ Rising Pune          │ ← from Set B
     │ KKR                  │ ← from Set B
     │ Kings XI Punjab      │ ← from Set B
     │ Mumbai Indians       │ ← from Set B
     │ Mumbai Indians       │ ← from Set B (kept!)
     │ RCB                  │ ← from Set B (kept!)
     └──────────────────────┘
```

**Syntax:**

```sql
SELECT column FROM TableA
UNION ALL
SELECT column FROM TableB;
```

***

**Example:**

```sql
SELECT winner FROM matches WHERE toss_decision = 'bat'
UNION ALL
SELECT winner FROM matches WHERE toss_decision = 'field';
```

**Result :** **every win listed including repeats:**

| winner                      |
| --------------------------- |
| Royal Challengers Bangalore |
| Delhi Daredevils            |
| Delhi Daredevils            |
| Royal Challengers Bangalore |
| Delhi Daredevils            |
| Sunrisers Hyderabad         |
| Rising Pune Supergiant      |
| Kolkata Knight Riders       |
| Kings XI Punjab             |
| Mumbai Indians              |
| Mumbai Indians              |
| Kolkata Knight Riders       |
| Mumbai Indians              |
| Sunrisers Hyderabad         |
| Mumbai Indians              |
| Kolkata Knight Riders       |
| Mumbai Indians              |
| Gujarat Lions               |
| Sunrisers Hyderabad         |
| Royal Challengers Bangalore |

> All 20 rows appear ,5 from Set A and 15 from Set B. Nothing removed.

**UNION vs UNION ALL**

|            | UNION                       | UNION ALL                          |
| ---------- | --------------------------- | ---------------------------------- |
| Duplicates |  Removed                    | Kept                               |
| Speed      | Slower (removes duplicates) | Faster                             |
| Use when   | Want unique results         | Want all results including repeats |

> 💡 If you already know there are no duplicates — use UNION ALL. It is faster because SQL does not have to check for duplicates.

### 3. INTERSECT

INTERSECT returns **only the rows that appear in BOTH query results** ,the common values.

**Visual Diagram:**

```
Set A                    Set B
┌──────────────────┐    ┌──────────────────┐
│ RCB              │    │ SRH              │
│ Delhi Daredevils │    │ Rising Pune      │
│                  │    │ KKR              │
│                  │    │ Kings XI Punjab  │
│                  │    │ Mumbai Indians   │
└──────────────────┘    │ RCB  ◄───────── │─┐
                        └──────────────────┘ │
                                             │
           INTERSECT Result                  │
         ┌──────────────┐                    │
         │ RCB          │◄───────────────────┘
         └──────────────┘
         Only what exists
         in BOTH sets
```

**Venn Diagram:**

```
        Set A              Set B
      ┌────────┐         ┌────────┐
      │  Delhi │  ┌───┐  │  SRH   │
      │        │  │RCB│  │  KKR   │
      │        │  └───┘  │ Mumbai │
      └────────┘         └────────┘
                  ↑
          INTERSECT =
          Only this common
          part returned
```

**Syntax:**

```sql
SELECT column FROM TableA
INTERSECT
SELECT column FROM TableB;
```

***

**Example:**

```sql
SELECT winner FROM matches WHERE toss_decision = 'bat'
INTERSECT
SELECT winner FROM matches WHERE toss_decision = 'field';
```

**Result :** **teams that won BOTH when batting first AND fielding first:**

| winner                      |
| --------------------------- |
| Royal Challengers Bangalore |

> Only RCB won matches in both situations ,batting first AND fielding first. All other teams won only in one situation.

### 4. EXCEPT

EXCEPT returns **rows from the FIRST query that do NOT appear in the SECOND query** , it subtracts one result from another.

**Visual Diagram:**

```
Set A                    Set B
┌──────────────────┐    ┌──────────────────┐
│ RCB          ────┼────►  (RCB exists     │
│ Delhi Daredevils │    │   here too,      │
│                  │    │   so removed)    │
└──────────────────┘    └──────────────────┘

        EXCEPT Result
    ┌──────────────────────┐
    │ Delhi Daredevils     │ ← Only in Set A, not in Set B
    └──────────────────────┘
```

**Venn Diagram:**

```
  Set A              Set B
  ┌────────┐         ┌────────┐
  │ Delhi  │  ┌───┐  │  SRH   │
  │████████│  │RCB│  │  KKR   │
  │████████│  └───┘  │ Mumbai │
  └────────┘         └────────┘
      ↑
EXCEPT =
Only Set A part
that is NOT in Set B
```

**Syntax:**

```sql
SELECT column FROM TableA
EXCEPT
SELECT column FROM TableB;
```

***

**Example:**

```sql
SELECT winner FROM matches WHERE toss_decision = 'bat'
EXCEPT
SELECT winner FROM matches WHERE toss_decision = 'field';
```

**Result : teams that won ONLY when batting first, never when fielding:**

| winner           |
| ---------------- |
| Delhi Daredevils |

> Delhi Daredevils won only when they batted first ,they never won when they fielded first. RCB is excluded because they appear in both sets.

**Reversing EXCEPT:**

```sql
SELECT winner FROM matches WHERE toss_decision = 'field'
EXCEPT
SELECT winner FROM matches WHERE toss_decision = 'bat';
```

**Result : teams that won ONLY when fielding first:**

| winner                 |
| ---------------------- |
| Sunrisers Hyderabad    |
| Rising Pune Supergiant |
| Kolkata Knight Riders  |
| Kings XI Punjab        |
| Mumbai Indians         |
| Gujarat Lions          |

> These teams only won when they chose to field first ,never when batting first.

#### All Set Operations -> Side by Side

```
   Set A    Set B        Set A    Set B
  ┌────┐   ┌────┐       ┌────┐   ┌────┐
  │    │███│    │       │████│███│████│
  │    │███│    │       │████│███│████│
  └────┘   └────┘       └────┘   └────┘
    UNION                 UNION ALL
  (no duplicates)      (keeps duplicates)

   Set A    Set B        Set A    Set B
  ┌────┐   ┌────┐       ┌────┐   ┌────┐
  │    │███│    │       │████│   │    │
  │    │███│    │       │████│   │    │
  └────┘   └────┘       └────┘   └────┘
   INTERSECT               EXCEPT
 (only common part)   (Set A minus Set B)
```

