---
hidden: true
---

# Views and Triggers

## What is a View?

A View is a **saved SELECT query that acts like a virtual table.** It does not store data itself ,it just stores the query. Every time you use the view, it runs that saved query and shows you the result.

Think of it like a **TV channel preset ,**&#x69;nstead of manually tuning to frequency 98.3 every time, you just press button 5 and it takes you there directly. A view is that button,press it and get your result instantly without writing the full query again.

You don’t store data again,you just **look at existing data in a different way**.

#### Why do we need Views?

Imagine you have this long complex query that you use every day:

```sql
SELECT winner,
       COUNT(*)            AS MatchesWon,
       AVG(win_by_runs)    AS AvgWinByRuns,
       MAX(win_by_runs)    AS BiggestWin
FROM matches
GROUP BY winner;
```

Without a view , you have to type this every single time.

With a view ,you save it once and just write:

```sql
SELECT * FROM WinnerSummary;
```

Done.

#### Visual Diagram -> How a View Works:

```
                    You write once
                         ↓
              ┌─────────────────────┐
              │       VIEW          │
              │   WinnerSummary     │
              │                     │
              │  SELECT winner,     │
              │  COUNT(*),          │
              │  AVG(win_by_runs)   │
              │  FROM matches       │
              │  GROUP BY winner    │
              └─────────────────────┘
                         ↓
              Every time you call it:
              SELECT * FROM WinnerSummary
                         ↓
              ┌─────────────────────┐
              │  winner  │ Wins │.. │
              │  Mumbai  │  4   │.. │
              │  Delhi   │  3   │.. │
              │  ...     │ ...  │.. │
              └─────────────────────┘
              Shows fresh result every time
```

### Creating a View

Syntax:

```sql
CREATE VIEW ViewName AS
SELECT query;
```

**Example -> Create a view that shows winner summary:**

```sql
CREATE VIEW WinnerSummary AS
SELECT winner,
       COUNT(*)            AS MatchesWon,
       AVG(win_by_runs)    AS AvgWinByRuns,
       MAX(win_by_runs)    AS BiggestWin
FROM matches
GROUP BY winner;
```

> View is now saved. You never have to write that long query again.

**Using the view just like a table:**

```sql
SELECT * FROM WinnerSummary;
```

#### Another View Example

**Create a view that shows only matches played in Hyderabad:**

```sql
CREATE VIEW HyderabadMatches AS
SELECT id, date, team1, team2, winner, player_of_match
FROM matches
WHERE city = 'Hyderabad';
```

**Using the view:**

```sql
SELECT * FROM HyderabadMatches;
```

> You can also add WHERE on top of a view:

```sql
SELECT * FROM HyderabadMatches
WHERE winner = 'Sunrisers Hyderabad';
```

#### Altering a View

Used when you want to **change the query inside an existing view** without dropping and recreating it.

**Syntax:**

```sql
ALTER VIEW ViewName AS
SELECT new_query;
```

**Example -> add city column to WinnerSummary view:**

```sql
ALTER VIEW WinnerSummary AS
SELECT winner,
       COUNT(*)            AS MatchesWon,
       AVG(win_by_runs)    AS AvgWinByRuns,
       MAX(win_by_runs)    AS BiggestWin,
       MIN(win_by_runs)    AS SmallestWin
FROM matches
GROUP BY winner;
```

> The view is now updated ,next time you call `SELECT * FROM WinnerSummary` it will include the new SmallestWin column.

#### Dropping a View

Used when you want to **completely delete a view.**

**Syntax:**

```sql
DROP VIEW ViewName;
```

**Example:**

```sql
DROP VIEW WinnerSummary;
DROP VIEW HyderabadMatches;
```

> Dropping a view only removes the saved query , **the actual data in the matches table is completely safe.** Nothing happens to the original table.

#### Important Things to Know About Views

***

**Views always show fresh data:**

A view does not store data , it stores only the query. So every time you call a view it **runs the query fresh** and shows the latest data from the original table.

```
matches table          View
┌──────────────┐      ┌──────────────┐
│ Original     │      │ No data      │
│ data lives   │◄─────│ stored here  │
│ here         │      │ Just a query │
└──────────────┘      └──────────────┘
       ↑
  Always reads
  fresh from here
```

**You can use a View just like a table:**

```sql
-- SELECT from a view
SELECT * FROM WinnerSummary;

-- Filter a view
SELECT * FROM WinnerSummary WHERE MatchesWon > 2;

-- Sort a view
SELECT * FROM WinnerSummary ORDER BY MatchesWon DESC;

-- Join a view with another table
SELECT W.winner, W.MatchesWon, M.city
FROM WinnerSummary W
JOIN matches M ON W.winner = M.winner;
```

**Why Views are useful (Summary):**

| Benefit          | Explanation                                  |
| ---------------- | -------------------------------------------- |
| **Simplicity**   | Hide complex queries behind a simple name    |
| **Reusability**  | Write once, use anywhere                     |
| **Security**     | Show only specific columns to specific users |
| **Fresh data**   | Always shows latest data from original table |
| **Cleaner code** | Queries become shorter and easier to read    |

## What is a Trigger?

A Trigger is a **special piece of SQL code that runs automatically** when something happens to a table  like when data is inserted, updated or deleted.

You do not call a trigger manually ,it fires on its own when the event happens.

Think of it like a **motion sensor light** ,you do not turn it on manually. It automatically turns on the moment someone walks in. A trigger works the same way ,the moment data changes, it automatically fires.

#### Visual Diagram -> How a Trigger Works:

```
  Someone runs:
  INSERT / UPDATE / DELETE
          ↓
  ┌───────────────────┐
  │     TABLE         │
  │   Data changes    │
  └───────────────────┘
          ↓
  ┌───────────────────┐
  │     TRIGGER       │◄── Fires automatically!
  │  (watching the    │    No manual call needed
  │   table always)   │
  └───────────────────┘
          ↓
  Automatic action happens
  (log it, update another
   table, send alert etc.)
```

#### Simple Table for Trigger Examples

We will use a simple Employee table:

```sql
CREATE TABLE Employee (
    ID       INT PRIMARY KEY,
    FullName VARCHAR(100),
    Salary   DECIMAL(10,2)
);

-- A log table to record changes
CREATE TABLE Employee_Log (
    LogID      INT IDENTITY(1,1),
    Action     VARCHAR(50),
    EmployeeID INT,
    LogTime    DATETIME DEFAULT GETDATE()
);
```

**Insert some data into Employee:**

```sql
INSERT INTO Employee VALUES (1, 'Rahul Sharma',  50000);
INSERT INTO Employee VALUES (2, 'Priya Verma',   45000);
INSERT INTO Employee VALUES (3, 'Amit Gupta',    60000);
INSERT INTO Employee VALUES (4, 'Sneha Patil',   55000);
INSERT INTO Employee VALUES (5, 'Ravi Shankar',  48000);
```

#### Types of Triggers

| Type           | When it fires            |
| -------------- | ------------------------ |
| `AFTER INSERT` | After a new row is added |
| `AFTER UPDATE` | After a row is changed   |
| `AFTER DELETE` | After a row is deleted   |

#### Full Syntax of a Trigger

```sql
CREATE TRIGGER TriggerName
ON TableName
AFTER INSERT / UPDATE / DELETE
AS
BEGIN
    -- your SQL code here
    -- what should happen automatically
END;
```

Breaking it down:

| Part                         | Meaning                          |
| ---------------------------- | -------------------------------- |
| `CREATE TRIGGER`             | Creates the trigger              |
| `TriggerName`                | Name you give the trigger        |
| `ON TableName`               | Which table to watch             |
| `AFTER INSERT/UPDATE/DELETE` | When should it fire              |
| `AS BEGIN ... END`           | What should happen when it fires |

#### The INSERTED and DELETED Tables

Before we write triggers you need to know about two special tables SQL Server gives you **inside every trigger:**

| Table      | Available in                   | Contains                                       |
| ---------- | ------------------------------ | ---------------------------------------------- |
| `inserted` | INSERT trigger, UPDATE trigger | The new rows that were just added or updated   |
| `deleted`  | DELETE trigger, UPDATE trigger | The old rows that were just removed or changed |

```
When INSERT happens:
┌──────────────┐      ┌──────────────┐
│   inserted   │      │   deleted    │
│  (new rows)  │      │   (empty)    │
└──────────────┘      └──────────────┘

When DELETE happens:
┌──────────────┐      ┌──────────────┐
│   inserted   │      │   deleted    │
│   (empty)    │      │  (old rows)  │
└──────────────┘      └──────────────┘

When UPDATE happens:
┌──────────────┐      ┌──────────────┐
│   inserted   │      │   deleted    │
│  (new rows   │      │  (old rows   │
│  after edit) │      │  before edit)│
└──────────────┘      └──────────────┘
```

> Think of UPDATE as  SQL first deletes the old row (goes into `deleted`) and then inserts the new row (goes into `inserted`).

#### 1. AFTER INSERT Trigger

Fires automatically **after a new row is inserted** into the table.

**Scenario:** Every time a new employee is added , automatically log it in Employee\_Log.

**Syntax:**

```sql
CREATE TRIGGER TriggerName
ON TableName
AFTER INSERT
AS
BEGIN
    -- use 'inserted' table to get the new row
    INSERT INTO LogTable (columns)
    SELECT columns
    FROM inserted;
END;
```

**Example:**

```sql
CREATE TRIGGER trg_AfterInsert
ON Employee
AFTER INSERT
AS
BEGIN
    INSERT INTO Employee_Log (Action, EmployeeID)
    SELECT 'New Employee Added', ID
    FROM inserted;
END;
```

**Testing the trigger:**

```sql
-- Insert a new employee
INSERT INTO Employee VALUES (6, 'Neha Singh', 52000);
```

**Check the log:**

```sql
SELECT * FROM Employee_Log;
```

**Result -> log was created automatically:**

| LogID | Action             | EmployeeID | LogTime             |
| ----- | ------------------ | ---------- | ------------------- |
| 1     | New Employee Added | 6          | 2024-03-25 14:35:22 |

> You never touched Employee\_Log -> the trigger did it automatically the moment INSERT happened.

#### 2. AFTER DELETE Trigger

Fires automatically **after a row is deleted** from the table.

**Scenario:** Every time an employee is deleted ,automatically log who was deleted.

**Syntax:**

```sql
CREATE TRIGGER TriggerName
ON TableName
AFTER DELETE
AS
BEGIN
    -- use 'deleted' table to get the removed row
    INSERT INTO LogTable (columns)
    SELECT columns
    FROM deleted;
END;
```

**Example:**

```sql
CREATE TRIGGER trg_AfterDelete
ON Employee
AFTER DELETE
AS
BEGIN
    INSERT INTO Employee_Log (Action, EmployeeID)
    SELECT 'Employee Deleted', ID
    FROM deleted;
END;
```

**Testing the trigger:**

```sql
-- Delete an employee
DELETE FROM Employee WHERE ID = 6;
```

**Check the log:**

```sql
SELECT * FROM Employee_Log;
```

**Result:**

| LogID | Action             | EmployeeID | LogTime             |
| ----- | ------------------ | ---------- | ------------------- |
| 1     | New Employee Added | 6          | 2024-03-25 14:35:22 |
| 2     | Employee Deleted   | 6          | 2024-03-25 15:10:45 |

> Deletion was automatically logged -> you did not write anything to Employee\_Log manually.

#### 3. AFTER UPDATE Trigger

Fires automatically **after a row is updated** in the table.

**Scenario:** Every time an employee record is updated ,automatically log what changed.

**Syntax:**

```sql
CREATE TRIGGER TriggerName
ON TableName
AFTER UPDATE
AS
BEGIN
    -- 'inserted' has new values
    -- 'deleted' has old values
    INSERT INTO LogTable (columns)
    SELECT columns
    FROM inserted;
END;
```

**Example:**

```sql
CREATE TRIGGER trg_AfterUpdate
ON Employee
AFTER UPDATE
AS
BEGIN
    INSERT INTO Employee_Log (Action, EmployeeID)
    SELECT 'Employee Updated', ID
    FROM inserted;
END;
```

**Testing the trigger:**

```sql
-- Update an employee salary
UPDATE Employee SET Salary = 70000 WHERE ID = 3;
```

**Check the log:**

```sql
SELECT * FROM Employee_Log;
```

**Result:**

| LogID | Action             | EmployeeID | LogTime             |
| ----- | ------------------ | ---------- | ------------------- |
| 1     | New Employee Added | 6          | 2024-03-25 14:35:22 |
| 2     | Employee Deleted   | 6          | 2024-03-25 15:10:45 |
| 3     | Employee Updated   | 3          | 2024-03-25 15:30:00 |

#### Altering a Trigger

Used to **modify an existing trigger** without dropping and recreating it.

```sql
ALTER TRIGGER trg_AfterInsert
ON Employee
AFTER INSERT
AS
BEGIN
    INSERT INTO Employee_Log (Action, EmployeeID)
    SELECT 'Employee Record Inserted', ID
    FROM inserted;
END;
```

#### Dropping a Trigger

Used to **completely remove a trigger.**

```sql
DROP TRIGGER trg_AfterInsert;
DROP TRIGGER trg_AfterDelete;
DROP TRIGGER trg_AfterUpdate;
DROP TRIGGER trg_InsteadOfDelete;
```

> Dropping a trigger only removes the trigger , the table and its data are completely safe.



> **Coming Up Next:** Imagine you are booking a movie ticket online and the payment goes through but the seat never gets confirmed. That is a transaction gone wrong. Next module we learn how SQL prevents exactly this using **Transactions and Exception Handling** ,making sure either everything happens or nothing happens at all!
