---
hidden: true
---

# DML Commands

> **Note:** We have already covered the **INSERT** command in our previous notes - how to add data into a table. Make sure you have gone through that before continuing.

> We will be using this **Employee Table** as our reference throughout all examples:

```sql
CREATE TABLE Employee (
    ID          INT           PRIMARY KEY,
    FullName    VARCHAR(100),
    Department  VARCHAR(50),
    DateOfJoining DATE,
    Gender      CHAR(1),
    EmailID     VARCHAR(150)
);
```

lets insert some data in our table first,

```sql
INSERT INTO Employee VALUES (1, 'Rahul Sharma',  'IT',      '2021-06-01', 'M', 'rahul.sharma@email.com');
INSERT INTO Employee VALUES (2, 'Priya Verma',   'HR',      '2022-03-15', 'F', 'priya.verma@email.com');
INSERT INTO Employee VALUES (3, 'Amit Gupta',    'Finance', '2020-11-20', 'M', 'amit.gupta@email.com');
INSERT INTO Employee VALUES (4, 'Sneha Patil',   'IT',      '2023-01-10', 'F', 'sneha.patil@email.com');
INSERT INTO Employee VALUES (5, 'Ravi Shankar',  'HR',      '2019-08-05', 'M', 'ravi.shankar@email.com');
```

After Inserting - Table Looks Like This:

| ID | FullName     | Department | DateOfJoining | Gender | EmailID                                                 |
| -- | ------------ | ---------- | ------------- | ------ | ------------------------------------------------------- |
| 1  | Rahul Sharma | IT         | 2021-06-01    | M      | [rahul.sharma@email.com](mailto:rahul.sharma@email.com) |
| 2  | Priya Verma  | HR         | 2022-03-15    | F      | [priya.verma@email.com](mailto:priya.verma@email.com)   |
| 3  | Amit Gupta   | Finance    | 2020-11-20    | M      | [amit.gupta@email.com](mailto:amit.gupta@email.com)     |
| 4  | Sneha Patil  | IT         | 2023-01-10    | F      | [sneha.patil@email.com](mailto:sneha.patil@email.com)   |
| 5  | Ravi Shankar | HR         | 2019-08-05    | M      | [ravi.shankar@email.com](mailto:ravi.shankar@email.com) |

as we have inserted data in our table,now we can perform other dml operations,let's study them one by one

## ALTER Command

The ALTER command is used to **change the structure of an existing table** , not the data inside it, but the table itself.

Think of it like this: You already built a shelf  and now you want to:

* Make one section wider
* Add a new section
* Remove a section

That is exactly what ALTER does to your table.

### 1. Modifying an Existing Column

Used when you want to **change something about an existing column** like increasing its size or changing its data type.

**Real-life scenario:** You created the `FullName` column with `VARCHAR(100)` but some employees have very long names and it is not fitting. So you want to increase the size to `VARCHAR(200)`.

```sql
ALTER TABLE Employee
ALTER COLUMN FullName VARCHAR(200);
```

**Before:**

| ID | FullName     | Department | DateOfJoining | Gender | EmailID                                                 |
| -- | ------------ | ---------- | ------------- | ------ | ------------------------------------------------------- |
| 1  | Rahul Sharma | IT         | 2021-06-01    | M      | [rahul.sharma@email.com](mailto:rahul.sharma@email.com) |
| 2  | Priya Verma  | HR         | 2022-03-15    | F      | [priya.verma@email.com](mailto:priya.verma@email.com)   |
| 3  | Amit Gupta   | Finance    | 2020-11-20    | M      | [amit.gupta@email.com](mailto:amit.gupta@email.com)     |
| 4  | Sneha Patil  | IT         | 2023-01-10    | F      | [sneha.patil@email.com](mailto:sneha.patil@email.com)   |
| 5  | Ravi Shankar | HR         | 2019-08-05    | M      | [ravi.shankar@email.com](mailto:ravi.shankar@email.com) |

**After:**

| ID | FullName (VARCHAR **200** now) | Department | DateOfJoining | Gender | EmailID                                                 |
| -- | ------------------------------ | ---------- | ------------- | ------ | ------------------------------------------------------- |
| 1  | Rahul Sharma                   | IT         | 2021-06-01    | M      | [rahul.sharma@email.com](mailto:rahul.sharma@email.com) |
| 2  | Priya Verma                    | HR         | 2022-03-15    | F      | [priya.verma@email.com](mailto:priya.verma@email.com)   |
| 3  | Amit Gupta                     | Finance    | 2020-11-20    | M      | [amit.gupta@email.com](mailto:amit.gupta@email.com)     |
| 4  | Sneha Patil                    | IT         | 2023-01-10    | F      | [sneha.patil@email.com](mailto:sneha.patil@email.com)   |
| 5  | Ravi Shankar                   | HR         | 2019-08-05    | M      | [ravi.shankar@email.com](mailto:ravi.shankar@email.com) |

> The **data did not change** - only the column size increased from 100 to 200. Think of it as making the box bigger.

## 2. Adding a New Column

Used when you want to **add a brand new column** to an existing table.

**Real-life scenario:** HR realized they forgot to add a `Salary` column when the table was first created. Now they want to add it without making the table all over again.

```sql
ALTER TABLE Employee
ADD Salary DECIMAL(10,2);
```

**Before:**

| ID | FullName     | Department | DateOfJoining | Gender | EmailID                                                 |
| -- | ------------ | ---------- | ------------- | ------ | ------------------------------------------------------- |
| 1  | Rahul Sharma | IT         | 2021-06-01    | M      | [rahul.sharma@email.com](mailto:rahul.sharma@email.com) |
| 2  | Priya Verma  | HR         | 2022-03-15    | F      | [priya.verma@email.com](mailto:priya.verma@email.com)   |
| 3  | Amit Gupta   | Finance    | 2020-11-20    | M      | [amit.gupta@email.com](mailto:amit.gupta@email.com)     |
| 4  | Sneha Patil  | IT         | 2023-01-10    | F      | [sneha.patil@email.com](mailto:sneha.patil@email.com)   |
| 5  | Ravi Shankar | HR         | 2019-08-05    | M      | [ravi.shankar@email.com](mailto:ravi.shankar@email.com) |

**After:**

| ID | FullName     | Department | DateOfJoining | Gender | EmailID                                                 | **Salary** |
| -- | ------------ | ---------- | ------------- | ------ | ------------------------------------------------------- | ---------- |
| 1  | Rahul Sharma | IT         | 2021-06-01    | M      | [rahul.sharma@email.com](mailto:rahul.sharma@email.com) | **NULL**   |
| 2  | Priya Verma  | HR         | 2022-03-15    | F      | [priya.verma@email.com](mailto:priya.verma@email.com)   | **NULL**   |
| 3  | Amit Gupta   | Finance    | 2020-11-20    | M      | [amit.gupta@email.com](mailto:amit.gupta@email.com)     | **NULL**   |
| 4  | Sneha Patil  | IT         | 2023-01-10    | F      | [sneha.patil@email.com](mailto:sneha.patil@email.com)   | **NULL**   |
| 5  | Ravi Shankar | HR         | 2019-08-05    | M      | [ravi.shankar@email.com](mailto:ravi.shankar@email.com) | **NULL**   |

> The new Salary column is added but all values are **NULL** — meaning empty — because we have not entered any salary yet. NULL just means "no value entered yet."

## 3. Deleting an Existing Column

Used when you want to **remove a column** you no longer need.

**Real-life scenario:** The company decided they do not want to store Gender anymore. So we remove that column.

```sql
ALTER TABLE Employee
DROP COLUMN Gender;
```

**Before:**

| ID | FullName     | Department | DateOfJoining | Gender | EmailID                                                 | Salary |
| -- | ------------ | ---------- | ------------- | ------ | ------------------------------------------------------- | ------ |
| 1  | Rahul Sharma | IT         | 2021-06-01    | **M**  | [rahul.sharma@email.com](mailto:rahul.sharma@email.com) | NULL   |
| 2  | Priya Verma  | HR         | 2022-03-15    | **F**  | [priya.verma@email.com](mailto:priya.verma@email.com)   | NULL   |
| 3  | Amit Gupta   | Finance    | 2020-11-20    | **M**  | [amit.gupta@email.com](mailto:amit.gupta@email.com)     | NULL   |
| 4  | Sneha Patil  | IT         | 2023-01-10    | **F**  | [sneha.patil@email.com](mailto:sneha.patil@email.com)   | NULL   |
| 5  | Ravi Shankar | HR         | 2019-08-05    | **M**  | [ravi.shankar@email.com](mailto:ravi.shankar@email.com) | NULL   |

**After:**

| ID | FullName     | Department | DateOfJoining | EmailID                                                 | Salary |
| -- | ------------ | ---------- | ------------- | ------------------------------------------------------- | ------ |
| 1  | Rahul Sharma | IT         | 2021-06-01    | [rahul.sharma@email.com](mailto:rahul.sharma@email.com) | NULL   |
| 2  | Priya Verma  | HR         | 2022-03-15    | [priya.verma@email.com](mailto:priya.verma@email.com)   | NULL   |
| 3  | Amit Gupta   | Finance    | 2020-11-20    | [amit.gupta@email.com](mailto:amit.gupta@email.com)     | NULL   |
| 4  | Sneha Patil  | IT         | 2023-01-10    | [sneha.patil@email.com](mailto:sneha.patil@email.com)   | NULL   |
| 5  | Ravi Shankar | HR         | 2019-08-05    | [ravi.shankar@email.com](mailto:ravi.shankar@email.com) | NULL   |

> The Gender column is completely gone — along with all the M and F values that were in it.  This cannot be undone.

### 4. DROP TABLE : Deleting the Entire Table

Used when you want to **completely delete the entire table** - the structure and all the data inside it.

**Real-life scenario:** You created a practice table called `Employee_Backup` for testing. Now you want to remove it completely.

sql

```sql
DROP TABLE Employee_Backup;
```

> This deletes everything — every column, every row, all data. The table completely disappears from the database.

**Before DROP:**

| ID  | FullName     | Department | ... |
| --- | ------------ | ---------- | --- |
| 1   | Rahul Sharma | IT         | ... |
| 2   | Priya Verma  | HR         | ... |
| ... | ...          | ...        | ... |

**After DROP:**

> &#x20;Table does not exist anymore. Nothing to show.

> &#x20;There is no undo for DROP TABLE. Always be 100% sure before running it.

## UPDATE Command

The UPDATE command is used to **change or edit existing data** inside a table.

Think of it like this: You filled a form  and later realized something was wrong , you go back and correct it. UPDATE does the same thing to your data.

```sql
UPDATE TableName
SET ColumnName = NewValue
WHERE condition;
```

### Example 1 — Updating One Column

Before we learn the right way, let us first see what happens when you forget the WHERE clause , so you never make this mistake.

**Scenario:** You want to update Rahul's department to Finance. But you forget to write WHERE.

```sql
UPDATE Employee
SET Department = 'Finance';
```

**Before:**

| ID | FullName     | Department | DateOfJoining | Gender | EmailID                                                 |
| -- | ------------ | ---------- | ------------- | ------ | ------------------------------------------------------- |
| 1  | Rahul Sharma | IT         | 2021-06-01    | M      | [rahul.sharma@email.com](mailto:rahul.sharma@email.com) |
| 2  | Priya Verma  | HR         | 2022-03-15    | F      | [priya.verma@email.com](mailto:priya.verma@email.com)   |
| 3  | Amit Gupta   | Finance    | 2020-11-20    | M      | [amit.gupta@email.com](mailto:amit.gupta@email.com)     |
| 4  | Sneha Patil  | IT         | 2023-01-10    | F      | [sneha.patil@email.com](mailto:sneha.patil@email.com)   |
| 5  | Ravi Shankar | HR         | 2019-08-05    | M      | [ravi.shankar@email.com](mailto:ravi.shankar@email.com) |

**After:**

| ID | FullName     | Department  | DateOfJoining | Gender | EmailID                                                 |
| -- | ------------ | ----------- | ------------- | ------ | ------------------------------------------------------- |
| 1  | Rahul Sharma | **Finance** | 2021-06-01    | M      | [rahul.sharma@email.com](mailto:rahul.sharma@email.com) |
| 2  | Priya Verma  | **Finance** | 2022-03-15    | F      | [priya.verma@email.com](mailto:priya.verma@email.com)   |
| 3  | Amit Gupta   | **Finance** | 2020-11-20    | M      | [amit.gupta@email.com](mailto:amit.gupta@email.com)     |
| 4  | Sneha Patil  | **Finance** | 2023-01-10    | F      | [sneha.patil@email.com](mailto:sneha.patil@email.com)   |
| 5  | Ravi Shankar | **Finance** | 2019-08-05    | M      | [ravi.shankar@email.com](mailto:ravi.shankar@email.com) |

> Every single employee is now in Finance — even HR and IT people. SQL updated **all rows** because you did not tell it which specific row to update.

### Always Use WHERE

WHERE tells SQL **which specific row** to update. Without it, SQL assumes you want to update everything.

```sql
UPDATE Employee
SET Department = 'Finance'
WHERE ID = 1;
```

**Before:**

| ID    | FullName     | Department | DateOfJoining | Gender | EmailID                                                 |
| ----- | ------------ | ---------- | ------------- | ------ | ------------------------------------------------------- |
| **1** | Rahul Sharma | **IT**     | 2021-06-01    | M      | [rahul.sharma@email.com](mailto:rahul.sharma@email.com) |
| 2     | Priya Verma  | HR         | 2022-03-15    | F      | [priya.verma@email.com](mailto:priya.verma@email.com)   |
| 3     | Amit Gupta   | Finance    | 2020-11-20    | M      | [amit.gupta@email.com](mailto:amit.gupta@email.com)     |
| 4     | Sneha Patil  | IT         | 2023-01-10    | F      | [sneha.patil@email.com](mailto:sneha.patil@email.com)   |
| 5     | Ravi Shankar | HR         | 2019-08-05    | M      | [ravi.shankar@email.com](mailto:ravi.shankar@email.com) |

**After:**

| ID    | FullName     | Department  | DateOfJoining | Gender | EmailID                                                 |
| ----- | ------------ | ----------- | ------------- | ------ | ------------------------------------------------------- |
| **1** | Rahul Sharma | **Finance** | 2021-06-01    | M      | [rahul.sharma@email.com](mailto:rahul.sharma@email.com) |
| 2     | Priya Verma  | HR          | 2022-03-15    | F      | [priya.verma@email.com](mailto:priya.verma@email.com)   |
| 3     | Amit Gupta   | Finance     | 2020-11-20    | M      | [amit.gupta@email.com](mailto:amit.gupta@email.com)     |
| 4     | Sneha Patil  | IT          | 2023-01-10    | F      | [sneha.patil@email.com](mailto:sneha.patil@email.com)   |
| 5     | Ravi Shankar | HR          | 2019-08-05    | M      | [ravi.shankar@email.com](mailto:ravi.shankar@email.com) |

> Only Rahul's row changed. Everyone else stayed exactly the same.

### Example 2 — Updating Multiple Columns at Once

**Scenario:** Priya Verma got married, her name changed and her email also changed. Update both at the same time.

```sql
UPDATE Employee
SET FullName = 'Priya Sharma',
    EmailID  = 'priya.sharma@email.com'
WHERE ID = 2;
```

**Before:**

| ID    | FullName        | Department | DateOfJoining | Gender | EmailID                                                   |
| ----- | --------------- | ---------- | ------------- | ------ | --------------------------------------------------------- |
| 1     | Rahul Sharma    | Finance    | 2021-06-01    | M      | [rahul.sharma@email.com](mailto:rahul.sharma@email.com)   |
| **2** | **Priya Verma** | HR         | 2022-03-15    | F      | [**priya.verma@email.com**](mailto:priya.verma@email.com) |
| 3     | Amit Gupta      | Finance    | 2020-11-20    | M      | [amit.gupta@email.com](mailto:amit.gupta@email.com)       |
| 4     | Sneha Patil     | IT         | 2023-01-10    | F      | [sneha.patil@email.com](mailto:sneha.patil@email.com)     |
| 5     | Ravi Shankar    | HR         | 2019-08-05    | M      | [ravi.shankar@email.com](mailto:ravi.shankar@email.com)   |

**After:**

| ID    | FullName         | Department | DateOfJoining | Gender | EmailID                                                     |
| ----- | ---------------- | ---------- | ------------- | ------ | ----------------------------------------------------------- |
| 1     | Rahul Sharma     | Finance    | 2021-06-01    | M      | [rahul.sharma@email.com](mailto:rahul.sharma@email.com)     |
| **2** | **Priya Sharma** | HR         | 2022-03-15    | F      | [**priya.sharma@email.com**](mailto:priya.sharma@email.com) |
| 3     | Amit Gupta       | Finance    | 2020-11-20    | M      | [amit.gupta@email.com](mailto:amit.gupta@email.com)         |
| 4     | Sneha Patil      | IT         | 2023-01-10    | F      | [sneha.patil@email.com](mailto:sneha.patil@email.com)       |
| 5     | Ravi Shankar     | HR         | 2019-08-05    | M      | [ravi.shankar@email.com](mailto:ravi.shankar@email.com)     |

> Both FullName and EmailID changed for Priya only. Everyone else was untouched.

## IDENTITY / Auto Increment

### The Problem First

Look at our current Employee table. Right now the `ID` column is a plain `INT PRIMARY KEY` ,meaning **we have to type the ID manually** every time we insert a new employee:

```sql
INSERT INTO Employee VALUES (1, 'Rahul Sharma',  'IT',      '2021-06-01', 'M', 'rahul.sharma@email.com');
INSERT INTO Employee VALUES (2, 'Priya Verma',   'HR',      '2022-03-15', 'F', 'priya.verma@email.com');
INSERT INTO Employee VALUES (3, 'Amit Gupta',    'Finance', '2020-11-20', 'M', 'amit.gupta@email.com');
INSERT INTO Employee VALUES (4, 'Sneha Patil',   'IT',      '2023-01-10', 'F', 'sneha.patil@email.com');
INSERT INTO Employee VALUES (5, 'Ravi Shankar',  'HR',      '2019-08-05', 'M', 'ravi.shankar@email.com');
```

This looks fine for 5 employees. But imagine you have **5000 employees** ,you would have to:

* Manually type every ID
* Remember what the last ID was
* Make sure you never repeat an ID

This is a lot of extra work and very easy to make mistakes like:

```sql
INSERT INTO Employee VALUES (4, 'Neha Singh', 'IT', '2023-05-01', 'F', 'neha@email.com');
-- ❌ Error! ID 4 already exists — Sneha Patil has ID 4
```

### The Solution - IDENTITY(start, step)

`IDENTITY` tells SQL Server _"You handle the ID yourself, generate it automatically, I will not type it manually."_

**Syntax:**

```sql
ColumnName INT IDENTITY(start, step)
```

* **start** → the number to begin from
* **step** → how much to increase each time a new row is added

### Creating the Table with IDENTITY

```sql
CREATE TABLE Employee (
    ID            INT IDENTITY(1,1) PRIMARY KEY,
    FullName      VARCHAR(100),
    Department    VARCHAR(50),
    DateOfJoining DATE,
    Gender        CHAR(1),
    EmailID       VARCHAR(150)
);
```

> `IDENTITY(1,1)` means — start from **1** and increase by **1** every time.

### Inserting Data — No Need to Type ID Anymore

Notice we are **not writing ID** in the INSERT statement at all:

```sql
INSERT INTO Employee (FullName, Department, DateOfJoining, Gender, EmailID)
VALUES ('Rahul Sharma',  'IT',      '2021-06-01', 'M', 'rahul.sharma@email.com');

INSERT INTO Employee (FullName, Department, DateOfJoining, Gender, EmailID)
VALUES ('Priya Verma',   'HR',      '2022-03-15', 'F', 'priya.verma@email.com');

INSERT INTO Employee (FullName, Department, DateOfJoining, Gender, EmailID)
VALUES ('Amit Gupta',    'Finance', '2020-11-20', 'M', 'amit.gupta@email.com');

INSERT INTO Employee (FullName, Department, DateOfJoining, Gender, EmailID)
VALUES ('Sneha Patil',   'IT',      '2023-01-10', 'F', 'sneha.patil@email.com');

INSERT INTO Employee (FullName, Department, DateOfJoining, Gender, EmailID)
VALUES ('Ravi Shankar',  'HR',      '2019-08-05', 'M', 'ravi.shankar@email.com');
```

**What the table looks like - ID filled automatically by SQL:**

| ID    | FullName     | Department | DateOfJoining | Gender | EmailID                                                 |
| ----- | ------------ | ---------- | ------------- | ------ | ------------------------------------------------------- |
| **1** | Rahul Sharma | IT         | 2021-06-01    | M      | [rahul.sharma@email.com](mailto:rahul.sharma@email.com) |
| **2** | Priya Verma  | HR         | 2022-03-15    | F      | [priya.verma@email.com](mailto:priya.verma@email.com)   |
| **3** | Amit Gupta   | Finance    | 2020-11-20    | M      | [amit.gupta@email.com](mailto:amit.gupta@email.com)     |
| **4** | Sneha Patil  | IT         | 2023-01-10    | F      | [sneha.patil@email.com](mailto:sneha.patil@email.com)   |
| **5** | Ravi Shankar | HR         | 2019-08-05    | M      | [ravi.shankar@email.com](mailto:ravi.shankar@email.com) |

> SQL automatically assigned ID 1, 2, 3, 4, 5 — you never typed a single ID.

### Playing with start and step

#### IDENTITY(1, 1) — Default, most common

```sql
ID INT IDENTITY(1,1)
-- Generates: 1, 2, 3, 4, 5...
```

| ID | FullName     |
| -- | ------------ |
| 1  | Rahul Sharma |
| 2  | Priya Verma  |
| 3  | Amit Gupta   |

#### IDENTITY(1001, 1) — Start from 1001

```sql
ID INT IDENTITY(1001,1)
-- Generates: 1001, 1002, 1003...
```

| ID   | FullName     |
| ---- | ------------ |
| 1001 | Rahul Sharma |
| 1002 | Priya Verma  |
| 1003 | Amit Gupta   |

> **Real-life example:** Many companies start employee IDs from 1001 so it looks more professional and does not start from 1.

#### IDENTITY(100, 10) — Increase by 10 each time

```sql
ID INT IDENTITY(100,10)
-- Generates: 100, 110, 120, 130...
```

| ID  | FullName     |
| --- | ------------ |
| 100 | Rahul Sharma |
| 110 | Priya Verma  |
| 120 | Amit Gupta   |

> **Real-life example:** Some systems leave gaps between IDs on purpose — so that related sub-records can be inserted in between later.

Once a number is used by IDENTITY, **it never repeats** even if you delete that row.

**Example:** If you delete the employee with ID 3 (Amit Gupta) and then insert a new employee - SQL will give the new employee ID **6**, not 3.

| ID    | FullName     | Department |
| ----- | ------------ | ---------- |
| 1     | Rahul Sharma | IT         |
| 2     | Priya Verma  | HR         |
| 4     | Sneha Patil  | IT         |
| 5     | Ravi Shankar | HR         |
| **6** | Neha Singh   | Finance    |

> ID 3 is gone forever. SQL does not reuse it. This is by design — to make sure every ID is always unique.
