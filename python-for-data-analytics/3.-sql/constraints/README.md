# Constraints

## What are Constraints?

Constraints are **rules applied to columns** in a table that control what kind of data can be entered. If someone tries to enter data that breaks a rule,SQL automatically rejects it.

Think of it like a **school admission form** :

* Roll number cannot be repeated,every student must have a unique one
* Name cannot be left blank
* Age must be between 5 and 20
* Class must be from a valid list

These are all constraints,rules that make sure wrong data never gets in.

## Our Table for Examples

We will create a **Student table** that uses all constraints together:

```sql
CREATE TABLE Student (
    StudentID   INT           PRIMARY KEY,
    FullName    VARCHAR(100)  NOT NULL,
    Email       VARCHAR(150)  UNIQUE,
    City        VARCHAR(50)   DEFAULT 'Delhi',
    Age         INT           CHECK (Age >= 5 AND Age <= 25),
    CourseID    INT           FOREIGN KEY REFERENCES Course(CourseID)
);
```

We will explain each constraint one by one using this table.

### 1. PRIMARY KEY Constraint

**What is a Primary Key?**

A Primary Key is a column that **uniquely identifies every row** in a table. No two rows can have the same Primary Key value and it can never be NULL.

Think of it like a **Aadhar Card number** ,every person has one, no two people share the same number and it can never be blank.

**Visual Diagram:**

```
Student Table
┌───────────┬──────────────┬─────────────────┐
│ StudentID │   FullName   │      Email      │
│ (PK)      │              │                 │
├───────────┼──────────────┼─────────────────┤
│    1      │ Rahul Sharma │ rahul@email.com │ 
│    2      │ Priya Verma  │ priya@email.com │ 
│    1      │ Amit Gupta   │ amit@email.com  │ ❌ Duplicate PK!
│   NULL    │ Sneha Patil  │ sneha@email.com │ ❌ NULL not allowed!
```

**Rules of Primary Key:**

| Rule           | Explanation                           |
| -------------- | ------------------------------------- |
| Unique         | No two rows can have same value       |
| Not NULL       | Cannot be empty ever                  |
| One per table  | A table can have only ONE primary key |
| Identifies row | Used to find any specific row         |

**Syntax -> Adding Primary Key:**

**While creating table:**

```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    FullName  VARCHAR(100)
);
```

**After creating table:**

```sql
ALTER TABLE Student
ADD CONSTRAINT PK_Student PRIMARY KEY (StudentID);
```

**Example:**

```sql
INSERT INTO Student VALUES (1, 'Rahul Sharma', ...); -- OK
INSERT INTO Student VALUES (2, 'Priya Verma',  ...); -- OK
INSERT INTO Student VALUES (1, 'Amit Gupta',   ...); -- ❌ Error! ID 1 already exists
INSERT INTO Student VALUES (NULL, 'Sneha',     ...); -- ❌ Error! NULL not allowed
```

### 2. NOT NULL Constraint

**What is NOT NULL?**

NOT NULL means a column **cannot be left empty** ,a value must always be provided.

Think of it like a form field marked with a \*\***red star** \*\*\* ,you cannot submit the form without filling it.

**Visual Diagram:**

```
Student Table — FullName has NOT NULL
┌───────────┬──────────────┐
│ StudentID │   FullName   │
│           │  (NOT NULL)  │
├───────────┼──────────────┤
│    1      │ Rahul Sharma │  Has a name
│    2      │ Priya Verma  │  Has a name
│    3      │    NULL      │  ❌ Not allowed!
│    4      │    ''        │  Empty string — allowed
└───────────┴──────────────┘
```

> NOT NULL prevents NULL but an empty string `''` is technically a value and is allowed. Be careful about this.

**Syntax:**

**While creating table:**

```sql
CREATE TABLE Student (
    StudentID INT     PRIMARY KEY,
    FullName  VARCHAR(100) NOT NULL
);
```

**After creating table:**

```sql
ALTER TABLE Student
ALTER COLUMN FullName VARCHAR(100) NOT NULL;
```

**Example:**

```sql
INSERT INTO Student (StudentID, FullName) VALUES (1, 'Rahul Sharma'); -- OK
INSERT INTO Student (StudentID, FullName) VALUES (2, NULL);           -- ❌ Error!
-- Cannot insert NULL into FullName column
```

### 3. UNIQUE Constraint

**What is UNIQUE?**

UNIQUE means **no two rows can have the same value** in that column , every value must be different.

Think of it like an **Email address** ,no two people can register with the same email on any website.

**Visual Diagram:**

```
Student Table — Email has UNIQUE constraint
┌───────────┬──────────────┬──────────────────────┐
│ StudentID │   FullName   │        Email         │
│           │              │      (UNIQUE)        │
├───────────┼──────────────┼──────────────────────┤
│    1      │ Rahul Sharma │  rahul@email.com     │ OK
│    2      │ Priya Verma  │  priya@email.com     │ OK
│    3      │ Amit Gupta   │  rahul@email.com     │ ❌ Duplicate!
│    4      │ Sneha Patil  │  NULL                │ NULL allowed
└───────────┴──────────────┴──────────────────────┘
```

**PRIMARY KEY vs UNIQUE Key Difference:**

|                     | PRIMARY KEY | UNIQUE                         |
| ------------------- | ----------- | ------------------------------ |
| Allows NULL?        |  Never      |  Yes (once)                    |
| How many per table? | Only ONE    | Multiple columns can be UNIQUE |
| Identifies row?     |  Yes        | Not necessarily                |
| Duplicate values?   |  Never      |  Never                         |

**Syntax:**

**While creating table:**

```sql
CREATE TABLE Student (
    StudentID INT          PRIMARY KEY,
    FullName  VARCHAR(100) NOT NULL,
    Email     VARCHAR(150) UNIQUE
);
```

**After creating table:**

```sql
ALTER TABLE Student
ADD CONSTRAINT UQ_Email UNIQUE (Email);
```

**Example:**

```sql
INSERT INTO Student VALUES (1, 'Rahul', 'rahul@email.com', ...); --  OK
INSERT INTO Student VALUES (2, 'Priya', 'priya@email.com', ...); --  OK
INSERT INTO Student VALUES (3, 'Amit',  'rahul@email.com', ...); -- ❌ Error!
-- Duplicate email not allowed
```

### 4. DEFAULT Constraint

**What is DEFAULT?**

DEFAULT means if no value is provided for a column ,SQL automatically fills it with a **pre-set default value.**

Think of it like a **pre-filled form,where** Country field is already filled as "India" ,you can change it if needed, but if you leave it blank it stays "India."

**Visual Diagram:**

```
Student Table — City has DEFAULT 'Delhi'

INSERT without City value:
┌───────────┬──────────────┬──────────┐
│ StudentID │   FullName   │   City   │
│           │              │(DEFAULT  │
│           │              │ 'Delhi') │
├───────────┼──────────────┼──────────┤
│    1      │ Rahul Sharma │  Delhi   │ ← Auto filled!
│    2      │ Priya Verma  │  Mumbai  │ ← Manually given
│    3      │ Amit Gupta   │  Delhi   │ ← Auto filled!
└───────────┴──────────────┴──────────┘
```

**Syntax:**

**While creating table:**

```sql
CREATE TABLE Student (
    StudentID INT           PRIMARY KEY,
    FullName  VARCHAR(100)  NOT NULL,
    City      VARCHAR(50)   DEFAULT 'Delhi'
);
```

**After creating table:**

```sql
ALTER TABLE Student
ADD CONSTRAINT DF_City DEFAULT 'Delhi' FOR City;
```

**Example:**

```sql
-- Provide city manually
INSERT INTO Student (StudentID, FullName, City)
VALUES (1, 'Rahul Sharma', 'Mumbai');
-- City = 'Mumbai' 

-- Do not provide city
INSERT INTO Student (StudentID, FullName)
VALUES (2, 'Priya Verma');
-- City = 'Delhi' automatically 
```

### 5. CHECK Constraint

**What is CHECK?**

CHECK sets a **condition that every value must satisfy** before it is accepted. If the value does not pass the condition then SQL rejects it.

Think of it like an **age verification** ,you must be above 18 to register. If you enter 15 then the form rejects it.

**Visual Diagram:**

```
Student Table — Age has CHECK (Age >= 5 AND Age <= 25)

┌───────────┬──────────────┬─────┐
│ StudentID │   FullName   │ Age │
│           │              │CHECK│
│           │              │5-25 │
├───────────┼──────────────┼─────┤
│    1      │ Rahul Sharma │ 20  │ Within range
│    2      │ Priya Verma  │  3  │ ❌ Below 5!
│    3      │ Amit Gupta   │ 30  │ ❌ Above 25!
│    4      │ Sneha Patil  │ 15  │ Within range
└───────────┴──────────────┴─────┘
```

**Syntax:**

**While creating table:**

```sql
CREATE TABLE Student (
    StudentID INT           PRIMARY KEY,
    FullName  VARCHAR(100)  NOT NULL,
    Age       INT           CHECK (Age >= 5 AND Age <= 25)
);
```

**After creating table:**

```sql
ALTER TABLE Student
ADD CONSTRAINT CHK_Age CHECK (Age >= 5 AND Age <= 25);
```

**More CHECK examples:**

```sql
-- Gender must be M or F only
Gender CHAR(1) CHECK (Gender IN ('M', 'F'))

-- Salary must be positive
Salary DECIMAL(10,2) CHECK (Salary > 0)

-- Marks between 0 and 100
Marks INT CHECK (Marks >= 0 AND Marks <= 100)
```

**Example:**

```sql
INSERT INTO Student VALUES (1, 'Rahul', 20, ...); -- Age 20 is valid
INSERT INTO Student VALUES (2, 'Priya',  3, ...); -- ❌ Error! Age 3 is below 5
INSERT INTO Student VALUES (3, 'Amit',  30, ...); -- ❌ Error! Age 30 is above 25
```

### 6. FOREIGN KEY Constraint

**What is a Foreign Key?**

A Foreign Key is a column in one table that **points to the Primary Key of another table** ,creating a link between the two tables.

This ensures that data in one table always **matches valid data in another table.** You cannot refer to something that does not exist.

**Real Life Example First:**

Think of a **library system** :

* **Book table** -> has all books with BookID
* **Borrow table** -> records who borrowed which book

When someone borrows a book ,you record the BookID in the Borrow table. But what if someone enters a BookID that does not exist? That is a problem.

**Foreign Key prevents this** ,it says _"BookID in Borrow table MUST exist in the Book table."_

#### **Visual Diagram -> How Foreign Key Works:**

```
Course Table (Parent Table)          Student Table (Child Table)
┌──────────┬─────────────┐          ┌───────────┬──────────┬──────────┐
│ CourseID │ CourseName  │          │ StudentID │FullName  │ CourseID │
│  (PK)    │             │          │  (PK)     │          │  (FK)    │
├──────────┼─────────────┤          ├───────────┼──────────┼──────────┤
│    1     │ Computer Sc │◄─────────│     1     │  Rahul   │    1     │ OK
│    2     │ Commerce    │◄─────────│     2     │  Priya   │    2     │ OK
│    3     │ Science     │◄─────────│     3     │  Amit    │    3     │ OK
└──────────┴─────────────┘          │     4     │  Sneha   │    9     │ ❌
                                    └───────────┴──────────┴──────────┘
                                    CourseID 9 does not exist
                                    in Course table — REJECTED!
```

**Parent Table and Child Table:**

| Term             | Meaning                                               |
| ---------------- | ----------------------------------------------------- |
| **Parent Table** | The table that has the Primary Key being referred to  |
| **Child Table**  | The table that has the Foreign Key pointing to parent |

```
Course Table          Student Table
 (Parent)      ←———      (Child) 
Has CourseID          Has CourseID as FK
```

> Parent table must be created FIRST before the child table.

**Creating the Tables:**

```sql
-- Step 1: Create Parent Table FIRST
CREATE TABLE Course (
    CourseID   INT          PRIMARY KEY,
    CourseName VARCHAR(100) NOT NULL
);

-- Step 2: Insert data into Parent Table
INSERT INTO Course VALUES (1, 'Computer Science');
INSERT INTO Course VALUES (2, 'Commerce');
INSERT INTO Course VALUES (3, 'Science');

-- Step 3: Create Child Table with Foreign Key
CREATE TABLE Student (
    StudentID INT           PRIMARY KEY,
    FullName  VARCHAR(100)  NOT NULL,
    Email     VARCHAR(150)  UNIQUE,
    City      VARCHAR(50)   DEFAULT 'Delhi',
    Age       INT           CHECK (Age >= 5 AND Age <= 25),
    CourseID  INT           FOREIGN KEY REFERENCES Course(CourseID)
);
```

**What Foreign Key Prevents:**

**1. You cannot insert a student with a CourseID that does not exist:**

```sql
INSERT INTO Student VALUES (1, 'Rahul', 'rahul@e.com', 'Delhi', 20, 1); --  CourseID 1 exists
INSERT INTO Student VALUES (2, 'Priya', 'priya@e.com', 'Mumbai', 22, 9); -- ❌ CourseID 9 
```

**2. You cannot delete a course that has students enrolled:**

```sql
DELETE FROM Course WHERE CourseID = 1;
-- ❌ Error! Rahul is still enrolled in CourseID 1
-- Cannot delete parent row that child is pointing to
```

**3. You cannot update a CourseID in Course table if students reference it:**

```sql
UPDATE Course SET CourseID = 99 WHERE CourseID = 1;
-- ❌ Error! Student table still references CourseID 1
```

&#x20;**What Happens Without/With Foreign Key:**

```
Without Foreign Key:
┌──────────┬─────────────┐     ┌───────────┬──────────┬──────────┐
│ CourseID │ CourseName  │     │ StudentID │FullName  │ CourseID │
├──────────┼─────────────┤     ├───────────┼──────────┼──────────┤
│    1     │ Computer Sc │     │     1     │  Rahul   │    1     │
│    2     │ Commerce    │     │     2     │  Priya   │    9     │ ← 9 does not exist!
│    3     │ Science     │     │     3     │  Amit    │   999    │ ← 999 does not exist!
└──────────┴─────────────┘     └───────────┴──────────┴──────────┘
         Orphan data! — Student enrolled in courses that do not exist
```

```
With Foreign Key:
┌──────────┬─────────────┐     ┌───────────┬──────────┬──────────┐
│ CourseID │ CourseName  │     │ StudentID │FullName  │ CourseID │
├──────────┼─────────────┤     ├───────────┼──────────┼──────────┤
│    1     │ Computer Sc │◄────│     1     │  Rahul   │    1     │ 
│    2     │ Commerce    │◄────│     2     │  Priya   │    2     │ 
│    3     │ Science     │◄────│     3     │  Amit    │    3     │ 
└──────────┴─────────────┘     └───────────┴──────────┴──────────┘
         Every student points to a real existing course 
```

**Syntax :** **Adding Foreign Key after table creation:**&#x20;

```sql
ALTER TABLE Student
ADD CONSTRAINT FK_CourseID
FOREIGN KEY (CourseID) REFERENCES Course(CourseID);
```

**Dropping a Foreign Key:**

```sql
ALTER TABLE Student
DROP CONSTRAINT FK_CourseID;
```

#### All Constraints Together :&#x20;

```sql
CREATE TABLE Course (
    CourseID   INT          PRIMARY KEY,
    CourseName VARCHAR(100) NOT NULL
);

CREATE TABLE Student (
    StudentID INT           PRIMARY KEY,         -- Unique ID, never NULL
    FullName  VARCHAR(100)  NOT NULL,             -- Name is required
    Email     VARCHAR(150)  UNIQUE,               -- No duplicate emails
    City      VARCHAR(50)   DEFAULT 'Delhi',      -- Auto fills Delhi if not given
    Age       INT           CHECK (Age >= 5       -- Age must be between 5 and 25
                                AND Age <= 25),
    CourseID  INT           FOREIGN KEY           -- Must exist in Course table
                            REFERENCES Course(CourseID)
);
```

> **Up Next:** Next module we cover **Window Functions, Moving Average and CTEs** , how to rank, compare and calculate across rows, how to smooth data over time and how to write cleaner and more readable complex queries.
