# Joins

## What are JOINs?

In real life, data is never stored in just one table. It is spread across multiple tables and sometimes you need to **combine data from two or more tables** to get the answer you need.

Think of it like this:

You have two registers in school :

* **Register 1**  has student names and their roll numbers
* **Register 2** has roll numbers and their marks

To find out which student got which marks you need to **connect both registers** using the roll number. That is exactly what JOIN does in SQL.



### We will use these two simple tables throughout to explain every join visually:

**Table A  -> Player**

| player\_id | player\_name |
| ---------- | ------------ |
| 1          | Virat Kohli  |
| 2          | Rohit Sharma |
| 3          | MS Dhoni     |
| 4          | KL Rahul     |

**Table B -> Awards**

| award\_id | player\_id | award\_name      |
| --------- | ---------- | ---------------- |
| 101       | 1          | Man of the Match |
| 102       | 2          | Best Batsman     |
| 103       | 5          | Best Bowler      |
| 104       | 3          | Best Captain     |

> Notice that player\_id 4 (KL Rahul) has no award. And award 103 has player\_id 5 which does not exist in the Player table. This is intentional and it helps show the difference between joins clearly.

### 1. INNER JOIN

INNER JOIN returns **only the rows that have matching values in BOTH tables.** If a row does not have a match in the other table then it is completely left out.

**Venn Diagram:**

```
    Table A          Table B
   ┌─────────┐     ┌─────────┐
   │         │█████│         │
   │  Only   │█████│  Only   │
   │    A    │█████│    B    │
   │         │█████│         │
   └─────────┘     └─────────┘
               ↑
         Only this
        middle part
        is returned
```

> INNER JOIN = **only the overlapping matching part** in the middle.

**Visual Table Explanation:**

| player\_id | Player Table  | Awards Table     | Included?            |
| ---------- | ------------- | ---------------- | -------------------- |
| 1          | Virat Kohli   | Man of the Match |  Match found         |
| 2          | Rohit Sharma  | Best Batsman     |  Match found         |
| 3          | MS Dhoni      | Best Captain     |  Match found         |
| 4          | KL Rahul      | No award         |  No match , left out |
| 5          | Not in Player | Best Bowler      |  No match , left out |

**Syntax:**

```sql
SELECT columns
FROM TableA
INNER JOIN TableB
ON TableA.common_column = TableB.common_column;
```

**Simple Example:**

```sql
SELECT P.player_name, A.award_name
FROM Player P
INNER JOIN Awards A
ON P.player_id = A.player_id;
```

**Result:**

| player\_name | award\_name      |
| ------------ | ---------------- |
| Virat Kohli  | Man of the Match |
| Rohit Sharma | Best Batsman     |
| MS Dhoni     | Best Captain     |

> KL Rahul is not here -> no matching award.\
> Best Bowler (player\_id 5) is not here -> no matching player.

**Practical Example -> IPL Tables:**

```sql
SELECT m.id, m.city, m.winner,
       d.batsman, d.batsman_runs
FROM matches m
INNER JOIN deliveries d
ON m.id = d.match_id
WHERE m.city = 'Hyderabad';
```

> This gives every delivery bowled in matches played in Hyderabad ,combining match info and delivery info together.

### 2. LEFT JOIN (LEFT OUTER JOIN)

LEFT JOIN returns **all rows from the LEFT table** and only the matching rows from the right table. If there is no match in the right table then the columns from the right table show as **NULL.**

**Venn Diagram:**

```
    Table A          Table B
   ┌─────────┐     ┌─────────┐
   │█████████│█████│         │
   │█████████│█████│  Only   │
   │  ALL OF │█████│    B    │
   │    A    │█████│         │
   └─────────┘     └─────────┘
        ↑
  Everything from
  LEFT table is
  always returned
```

> LEFT JOIN = **everything from left table** + matching rows from right table.

**Visual Table Explanation:**

| player\_id | Player Table  | Awards Table     | Included?                         |
| ---------- | ------------- | ---------------- | --------------------------------- |
| 1          | Virat Kohli   | Man of the Match |  Match found                      |
| 2          | Rohit Sharma  | Best Batsman     |  Match found                      |
| 3          | MS Dhoni      | Best Captain     |  Match found                      |
| 4          | KL Rahul      | NULL             |  Included , but award is NULL     |
| 5          | Not in Player | Best Bowler      |  Not included . not in left table |

**Syntax:**

```sql
SELECT columns
FROM TableA
LEFT JOIN TableB
ON TableA.common_column = TableB.common_column;
```

***

**Simple Example:**

```sql
SELECT P.player_name, A.award_name
FROM Player P
LEFT JOIN Awards A
ON P.player_id = A.player_id;
```

**Result:**

| player\_name | award\_name      |
| ------------ | ---------------- |
| Virat Kohli  | Man of the Match |
| Rohit Sharma | Best Batsman     |
| MS Dhoni     | Best Captain     |
| KL Rahul     | NULL             |

> KL Rahul is now included but award\_name is NULL because he has no award. Best Bowler (player\_id 5) is still not here as it is not in the LEFT table.

**Finding rows with NO match  :**

```sql
SELECT P.player_name, A.award_name
FROM Player P
LEFT JOIN Awards A
ON P.player_id = A.player_id
WHERE A.award_name IS NULL;
```

**Result:**

| player\_name | award\_name |
| ------------ | ----------- |
| KL Rahul     | NULL        |

> This is a very common real-life use , finding players who have NO award, customers who have NO orders, employees who have NO department etc.

**Practical Example -> IPL Tables:**

```sql
SELECT m.id, m.city, m.winner,
       d.batsman, d.batsman_runs
FROM matches m
LEFT JOIN deliveries d
ON m.id = d.match_id;
```

> Returns all matches , even those that have no delivery data recorded. Delivery columns will show NULL for those matches.

### 3. RIGHT JOIN (RIGHT OUTER JOIN)

RIGHT JOIN is the **opposite of LEFT JOIN** , it returns **all rows from the RIGHT table** and only the matching rows from the left table. If there is no match in the left table then left table columns show as **NULL.**

**Venn Diagram:**

```
    Table A          Table B
   ┌─────────┐     ┌─────────┐
   │         │█████│█████████│
   │  Only   │█████│█████████│
   │    A    │█████│  ALL OF │
   │         │█████│    B    │
   └─────────┘     └─────────┘
                        ↑
                 Everything from
                 RIGHT table is
                 always returned
```

> RIGHT JOIN = **everything from right table** + matching rows from left table.

**Visual Table Explanation:**

| player\_id | Player Table | Awards Table     | Included?                          |
| ---------- | ------------ | ---------------- | ---------------------------------- |
| 1          | Virat Kohli  | Man of the Match |  Match found                       |
| 2          | Rohit Sharma | Best Batsman     |  Match found                       |
| 3          | MS Dhoni     | Best Captain     |  Match found                       |
| 4          | KL Rahul     | No award         |  Not included ,not in right table  |
| 5          | NULL         | Best Bowler      |  Included ,but player name is NULL |

**Syntax:**

```sql
SELECT columns
FROM TableA
RIGHT JOIN TableB
ON TableA.common_column = TableB.common_column;
```

***

**Simple Example:**

```sql
SELECT P.player_name, A.award_name
FROM Player P
RIGHT JOIN Awards A
ON P.player_id = A.player_id;
```

**Result:**

| player\_name | award\_name      |
| ------------ | ---------------- |
| Virat Kohli  | Man of the Match |
| Rohit Sharma | Best Batsman     |
| MS Dhoni     | Best Captain     |
| **NULL**     | Best Bowler      |

> Best Bowler is now included but player\_name is NULL because player\_id 5 does not exist in the Player table. KL Rahul is gone as he has no award so he is not in the right table.

**Practical Example -> IPL Tables:**

```sql
SELECT m.id, m.city, m.winner,
       d.batsman, d.batsman_runs
FROM matches m
RIGHT JOIN deliveries d
ON m.id = d.match_id;
```

> Returns all deliveries even those whose match\_id does not exist in the matches table. Match columns will show NULL for those deliveries.

### 4. FULL OUTER JOIN

FULL OUTER JOIN returns **everything from BOTH tables** ,matched rows together and unmatched rows from both sides with NULL where there is no match.

Think of it like combining both LEFT JOIN and RIGHT JOIN together.

**Venn Diagram:**

```
    Table A          Table B
   ┌─────────┐     ┌─────────┐
   │█████████│█████│█████████│
   │█████████│█████│█████████│
   │  ALL OF │█████│  ALL OF │
   │    A    │█████│    B    │
   └─────────┘     └─────────┘
         ↑               ↑
    Everything      Everything
    from A          from B
```

> FULL OUTER JOIN = **everything from both tables** ,matched and unmatched.

**Visual Table Explanation:**

| player\_id | Player Table | Awards Table     | Included?                    |
| ---------- | ------------ | ---------------- | ---------------------------- |
| 1          | Virat Kohli  | Man of the Match |  Match found                 |
| 2          | Rohit Sharma | Best Batsman     | Match found                  |
| 3          | MS Dhoni     | Best Captain     |  Match found                 |
| 4          | KL Rahul     | **NULL**         |  From left , award is NULL   |
| 5          | **NULL**     | Best Bowler      |  From right , player is NULL |

**Syntax:**

```sql
SELECT columns
FROM TableA
FULL OUTER JOIN TableB
ON TableA.common_column = TableB.common_column;
```

**Simple Example:**

```sql
SELECT P.player_name, A.award_name
FROM Player P
FULL OUTER JOIN Awards A
ON P.player_id = A.player_id;
```

**Result:**

| player\_name | award\_name      |
| ------------ | ---------------- |
| Virat Kohli  | Man of the Match |
| Rohit Sharma | Best Batsman     |
| MS Dhoni     | Best Captain     |
| KL Rahul     | NULL             |
| NULL         | Best Bowler      |

> Everyone from both tables is included. NULLs appear where there is no match.

**Practical Example -> IPL Tables:**

```sql
SELECT m.id, m.city, m.winner,
       d.batsman, d.batsman_runs
FROM matches m
FULL OUTER JOIN deliveries d
ON m.id = d.match_id;
```

> Returns everything , all matches and all deliveries. NULLs appear wherever there is no match on either side.

### 5. SELF JOIN

A SELF JOIN is when a table **joins with itself.** This sounds strange but it is useful when a table has a column that references another row in the same table.

Think of it like this: You have an Employee table where each employee has a `manager_id`  and that manager is also an employee in the same table. To find who manages whom ,you join the table with itself.

**Simple Tables for Self Join:**

**Employee Table:**

| emp\_id | emp\_name | manager\_id |
| ------- | --------- | ----------- |
| 1       | Rahul     | 3           |
| 2       | Priya     | 3           |
| 3       | Amit      | NULL        |
| 4       | Sneha     | 2           |

> Amit (ID 3) is the manager of Rahul and Priya. Priya (ID 2) is the manager of Sneha. Amit has no manager as he is the top.

**Venn Diagram:**

```
      Table A                  Table A
   (as Employee)            (as Manager)
   ┌─────────┐              ┌─────────┐
   │█████████│██████████████│█████████│
   │  emp_id │◄─────────────│manager_│
   │ emp_name│  same table  │  id    │
   └─────────┘  joined on   └─────────┘
                itself
```

> Same table used twice ,once as Employee, once as Manager.

**Syntax:**

```sql
SELECT A.column, B.column
FROM TableA A
JOIN TableA B
ON A.column = B.column;
```

**Simple Example:**

```sql
SELECT E.emp_name AS Employee,
       M.emp_name AS Manager
FROM Employee E
LEFT JOIN Employee M
ON E.manager_id = M.emp_id;
```

**Result:**

| Employee | Manager |
| -------- | ------- |
| Rahul    | Amit    |
| Priya    | Amit    |
| Amit     | NULL    |
| Sneha    | Priya   |

> Amit shows NULL as manager because he has no manager. Everyone else shows their manager's name correctly.

### 6. CROSS JOIN

CROSS JOIN combines **every row from Table A with every row from Table B** ,giving every possible combination. There is no **ON** condition needed.

Think of it like this: You have 3 T-shirt colors and 3 sizes and  CROSS JOIN gives you all 9 possible combinations (Small-Red, Small-Blue, Small-Green, Medium-Red... and so on).

**Venn Diagram:**

```
    Table A          Table B
   ┌─────────┐     ┌─────────┐
   │  Row 1  │────►│  Row 1  │
   │  Row 1  │────►│  Row 2  │
   │  Row 2  │────►│  Row 1  │
   │  Row 2  │────►│  Row 2  │
   │  Row 3  │────►│  Row 1  │
   │  Row 3  │────►│  Row 2  │
   └─────────┘     └─────────┘
      Every row in A
      pairs with every
      row in B
```

> If Table A has 4 rows and Table B has 4 rows then CROSS JOIN gives 4 × 4 = **16 rows.**

**Syntax:**

```sql
SELECT columns
FROM TableA
CROSS JOIN
TableB;
```

***

**Simple Example:**

```sql
SELECT P.player_name, A.award_name
FROM Player P
CROSS JOIN Awards A;
```

> Every player is paired with every award whether they won it or not.

**Practical Example — IPL Tables:**

sql

```sql
SELECT DISTINCT m.city, d.bowling_team
FROM matches m
CROSS JOIN deliveries d;
```

> Every city is combined with every bowling team giving all possible city and team combinations.

> Be careful with CROSS JOIN on large tables , if matches has 756 rows and deliveries has 179,000 rows, CROSS JOIN will produce **756 × 179,000 = 135 million rows.** Always use on small datasets or with filters.

#### All Joins -> Side by Side Comparison

```
INNER JOIN          LEFT JOIN           RIGHT JOIN        FULL OUTER JOIN
┌────┐  ┌────┐    ┌────┐  ┌────┐    ┌────┐  ┌────┐    ┌────┐  ┌────┐
│    │██│    │    │████│██│    │    │    │██│████│    │████│██│████│
│    │██│    │    │████│██│    │    │    │██│████│    │████│██│████│
└────┘  └────┘    └────┘  └────┘    └────┘  └────┘    └────┘  └────┘
 Only matching      All of Left +    All of Right +    Everything from
 rows from both     matching Right   matching Left     both tables
```



> **Up Next:** In the next module we will cover **Set Operations** : UNION, UNION ALL, INTERSECT and EXCEPT. These are used to combine results of two or more SELECT queries directly without using joins.



