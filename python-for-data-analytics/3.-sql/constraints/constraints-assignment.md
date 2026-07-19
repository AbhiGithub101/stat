---
description: Practice SQL Server constraints
---

# Constraints Assignment

### Practice dataset

A training institute manages courses and student enrollments. The `Course` table is the parent table. The `Student` table is the child table.

```sql
CREATE TABLE Course (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(100) NOT NULL
);

CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    FullName VARCHAR(100) NOT NULL,
    Email VARCHAR(150) UNIQUE,
    City VARCHAR(50) DEFAULT 'Delhi',
    Age INT CHECK (Age >= 5 AND Age <= 25),
    CourseID INT FOREIGN KEY REFERENCES Course(CourseID)
);

INSERT INTO Course (CourseID, CourseName)
VALUES
    (101, 'SQL Fundamentals'),
    (102, 'Data Analytics'),
    (103, 'Business Intelligence');

INSERT INTO Student (StudentID, FullName, Email, City, Age, CourseID)
VALUES
    (1001, 'Aisha Khan', 'aisha@learnpro.com', 'Delhi', 21, 101),
    (1002, 'Rohan Mehta', 'rohan@learnpro.com', 'Mumbai', 23, 102),
    (1004, 'Kabir Das', 'kabir@learnpro.com', 'Pune', 25, 103);

INSERT INTO Student (StudentID, FullName, Email, Age, CourseID)
VALUES (1003, 'Neha Singh', 'neha@learnpro.com', 20, 101);
```

> Run each data-changing question separately. Some statements are designed to fail.

### Primary key and NOT NULL

#### 1. Write an `INSERT` statement that tries to add `Aman Roy` with `StudentID` `1001`. Use a valid email, city, age, and course. Will SQL Server accept it?

<details>

<summary>Solution</summary>

```sql
INSERT INTO Student (StudentID, FullName, Email, City, Age, CourseID)
VALUES (1001, 'Aman Roy', 'aman@learnpro.com', 'Delhi', 22, 101);
```

SQL Server rejects this statement. `StudentID` `1001` already exists.

</details>

#### 2. Which constraint prevents both duplicate values and `NULL` values?

* A. `DEFAULT`
* B. `CHECK`
* C. `PRIMARY KEY`
* D. `UNIQUE`

<details>

<summary>Solution</summary>

**C. `PRIMARY KEY`**. It uniquely identifies each row and never allows `NULL`.

</details>

### UNIQUE and DEFAULT

#### 3. Insert student `1005`, `Dev Patel`, and a valid age and course. Omit `City` from the column list. Then write a query to verify the saved city.

<details>

<summary>Solution</summary>

```sql
INSERT INTO Student (StudentID, FullName, Email, Age, CourseID)
VALUES (1005, 'Dev Patel', 'dev@learnpro.com', 24, 102);

SELECT StudentID, FullName, City
FROM Student
WHERE StudentID = 1005;
```

The query returns `Delhi` for `City`.

</details>

#### 4. A `DEFAULT` value is used when a column is \_\_\_\_\_\_\_\_\_\_ from an `INSERT` statement.

<details>

<summary>Solution</summary>

**omitted**

The default applies when no value is supplied for that column.

</details>

### CHECK constraints

#### 5. The `Age` column has `CHECK (Age >= 5 AND Age <= 25)`. Which ages are valid: `4`, `5`, `25`, and `26`?

<details>

<summary>Solution</summary>

`5` and `25` are valid. The condition includes both boundary values.

`4` and `26` are invalid.

</details>

#### 6. Write an `INSERT` statement for student `1006`, `Ira Bose`, with age `26`. Use valid values for every other column. Explain the result.

<details>

<summary>Solution</summary>

```sql
INSERT INTO Student (StudentID, FullName, Email, City, Age, CourseID)
VALUES (1006, 'Ira Bose', 'ira@learnpro.com', 'Kolkata', 26, 103);
```

SQL Server rejects the insert. Age `26` fails the `CHECK` condition.

</details>

#### 7. **True or False:** A `CHECK` constraint can restrict a numeric value to a defined range.

<details>

<summary>Solution</summary>

**True.** The `Age` constraint restricts values from `5` through `25`.

</details>

### Foreign keys

#### 8. Identify the parent table, child table, parent key, and foreign key in the shared dataset.

<details>

<summary>Solution</summary>

* Parent table: `Course`
* Child table: `Student`
* Parent key: `Course.CourseID`
* Foreign key: `Student.CourseID`

</details>

#### 9. Try to insert student `1007`, `Sara Ali`, with `CourseID` `999`. Use valid values for all other columns. What happens?

<details>

<summary>Solution</summary>

```sql
INSERT INTO Student (StudentID, FullName, Email, City, Age, CourseID)
VALUES (1007, 'Sara Ali', 'sara@learnpro.com', 'Delhi', 19, 999);
```

SQL Server rejects the insert. Course `999` does not exist in `Course`.

</details>

#### 10. Which statement correctly describes a foreign key?

* A. It supplies a value when a column is omitted.
* B. It links a child column to a key in another table.
* C. It allows only positive numbers.
* D. It automatically sorts table rows.

<details>

<summary>Solution</summary>

**B. It links a child column to a key in another table.**

</details>

### Adding constraints after creation

#### 11. Add a named `CHECK` constraint called `CHK_Student_City`. It must allow only `Delhi`, `Mumbai`, `Pune`, or `Kolkata` in `Student.City`.

<details>

<summary>Solution</summary>

```sql
ALTER TABLE Student
ADD CONSTRAINT CHK_Student_City
CHECK (City IN ('Delhi', 'Mumbai', 'Pune', 'Kolkata'));
```

All existing cities satisfy this new rule.

</details>

#### 12. Complete the statement that adds a unique constraint to `CourseName`.

```sql
ALTER TABLE Course
ADD CONSTRAINT UQ_Course_CourseName ________ (CourseName);
```

<details>

<summary>Solution</summary>

```sql
ALTER TABLE Course
ADD CONSTRAINT UQ_Course_CourseName UNIQUE (CourseName);
```

</details>

### Constraint scenarios

#### 13. A learner enters an empty string (`''`) for `FullName`. Does `NOT NULL` reject it? ( YES / NO )

<details>

<summary>Solution</summary>

No. `NOT NULL` rejects only `NULL`. An empty string is still a value.

</details>

#### 14. **True or False:** SQL Server can delete a parent row while child rows still reference it through a foreign key.

<details>

<summary>Solution</summary>

**False.** The foreign key prevents the delete while matching student rows exist.

</details>

#### 15. Insert `Meera Iyer` as student `1008`. Use `meera@learnpro.com`, age `25`, and course `103`. Do not supply `City`. Then return the new row.

<details>

<summary>Solution</summary>

```sql
INSERT INTO Student (StudentID, FullName, Email, Age, CourseID)
VALUES (1008, 'Meera Iyer', 'meera@learnpro.com', 25, 103);

SELECT StudentID, FullName, Email, City, Age, CourseID
FROM Student
WHERE StudentID = 1008;
```

The insert succeeds. The row receives `Delhi` as its city.

</details>

#### 16. Write three separate `INSERT` statements for new students. Each must fail for a different reason:

1. Duplicate email
2. Missing `FullName`
3. Invalid `CourseID`

<details>

<summary>Solution</summary>

```sql
-- Duplicate email
INSERT INTO Student (StudentID, FullName, Email, City, Age, CourseID)
VALUES (1009, 'Vikram Shah', 'aisha@learnpro.com', 'Delhi', 22, 101);

-- Missing FullName
INSERT INTO Student (StudentID, FullName, Email, City, Age, CourseID)
VALUES (1010, NULL, 'tara@learnpro.com', 'Delhi', 20, 102);

-- Invalid CourseID
INSERT INTO Student (StudentID, FullName, Email, City, Age, CourseID)
VALUES (1011, 'Nikhil Jain', 'nikhil@learnpro.com', 'Delhi', 20, 999);
```

The statements fail because of `UNIQUE`, `NOT NULL`, and `FOREIGN KEY` constraints, respectively.

</details>

#### 17. Which insert succeeds with the original shared dataset?

* A. `StudentID = 1001`, valid remaining values
* B. `FullName = NULL`, valid remaining values
* C. `Age = 4`, valid remaining values
* D. `StudentID = 1012`, valid remaining values, and `CourseID = 102`

<details>

<summary>Solution</summary>

**D.** `StudentID` `1012` is new, and course `102` exists. The values meet all constraints.

</details>
