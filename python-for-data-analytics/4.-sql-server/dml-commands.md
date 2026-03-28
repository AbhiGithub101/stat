# DML Commands

> **Note:** We have already covered the **INSERT** command in our previous notes — how to add data into a table. Make sure you have gone through that before continuing.

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
