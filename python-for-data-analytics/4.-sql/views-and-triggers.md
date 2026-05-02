---
hidden: true
---

# Views and Triggers

## What is a View?

* A **View is a virtual table** created from a query.
* A view is like a **saved result of a SELECT query**

You don’t store data again,you just **look at existing data in a different way**.

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

### Real-Life Example

Think of a school database:

| ID | Name  | Marks | Section |
| -- | ----- | ----- | ------- |
| 1  | Suraj | 85    | A       |
| 2  | Ravi  | 40    | B       |
| 3  | Neha  | 90    | A       |

Now teacher only wants to see **students who passed (marks ≥ 50)**

Instead of writing query again and again, we create a VIEW.

```sql
CREATE VIEW passed_students AS
SELECT name, marks
FROM students
WHERE marks >= 50;
```

### What this means in simple language:

&#x20;Make a virtual table called `passed_students`\
that shows only name and marks\
for students who scored 50 or more.”

### How to use the VIEW

After creating it, you use it like a normal table:

```sql
SELECT * FROM passed_students;
```

Output:

| name  | marks |
| ----- | ----- |
| Suraj | 85    |
| Neha  | 90    |
