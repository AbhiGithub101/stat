---
hidden: true
---

# Transactions and Exception Handling Assignment

### Practice dataset

```sql
CREATE TABLE Accounts (
    AccountID INT PRIMARY KEY,
    AccountHolder VARCHAR(100),
    Balance DECIMAL(12, 2)
);

INSERT INTO Accounts (AccountID, AccountHolder, Balance)
VALUES
(101, 'Aditi Sharma', 25000.00),
(102, 'Rohan Mehta', 18000.00),
(103, 'Neha Kapoor', 12500.00),
(104, 'Kabir Singh', 9000.00);
```

Use the `Accounts` table for every query.

### Transactions

#### 1. Which command starts a transaction?

* A. `START`
* B. `BEGIN TRANSACTION`
* C. `OPEN TRANSACTION`
* D. `CREATE TRANSACTION`

<details>

<summary>Solution</summary>

**B. `BEGIN TRANSACTION`**

It marks the start of a transaction.

</details>

#### 2. Complete the statement that permanently saves the changes.

```sql
BEGIN TRANSACTION;

UPDATE Accounts
SET Balance = Balance + 1000
WHERE AccountID = 101;

________;
```

<details>

<summary>Solution</summary>

```sql
COMMIT;
```

`COMMIT` saves transaction changes permanently.

</details>

#### 3. `ROLLBACK` permanently saves every change made in a transaction. True or False?

<details>

<summary>Solution</summary>

**False.**

`ROLLBACK` undoes changes made since `BEGIN TRANSACTION`.

</details>

#### 4. A payment system deducts `2000.00` from Aditi's account. It adds the same amount to Rohan's account. Write the transaction.

<details>

<summary>Solution</summary>

```sql
BEGIN TRANSACTION;

UPDATE Accounts
SET Balance = Balance - 2000.00
WHERE AccountID = 101;

UPDATE Accounts
SET Balance = Balance + 2000.00
WHERE AccountID = 102;

COMMIT;
```

Both balance updates are saved together.

</details>

#### 5. Write a transaction that adds `500.00` to Neha's account. Undo the change before it is saved.

<details>

<summary>Solution</summary>

```sql
BEGIN TRANSACTION;

UPDATE Accounts
SET Balance = Balance + 500.00
WHERE AccountID = 103;

ROLLBACK;
```

Neha's balance remains unchanged.

</details>

#### 6. What happens after this script runs?

```sql
BEGIN TRANSACTION;

UPDATE Accounts
SET Balance = Balance - 1000.00
WHERE AccountID = 104;

ROLLBACK;
```

<details>

<summary>Solution</summary>

Kabir's balance stays unchanged at `9000.00`.

`ROLLBACK` undoes the update.

</details>

#### 7. A transfer moves `1500.00` from Rohan to Neha. Write one transaction. Display all accounts after the transaction completes.

<details>

<summary>Solution</summary>

```sql
BEGIN TRANSACTION;

UPDATE Accounts
SET Balance = Balance - 1500.00
WHERE AccountID = 102;

UPDATE Accounts
SET Balance = Balance + 1500.00
WHERE AccountID = 103;

COMMIT;

SELECT *
FROM Accounts;
```

The `SELECT` confirms the committed balances.

</details>

### Exception handling

#### 8. Which block runs when an error occurs inside `TRY`?

* A. `BEGIN ERROR`
* B. `BEGIN CATCH`
* C. `BEGIN ROLLBACK`
* D. `BEGIN PRINT`

<details>

<summary>Solution</summary>

**B. `BEGIN CATCH`**

SQL Server moves to the `CATCH` block after an error in `TRY`.

</details>

#### 9. Complete the missing keywords.

```sql
BEGIN _____
    PRINT 100 / 0;
END _____
BEGIN _____
    PRINT 'An error occurred.';
END _____
```

<details>

<summary>Solution</summary>

```sql
BEGIN TRY
    PRINT 100 / 0;
END TRY
BEGIN CATCH
    PRINT 'An error occurred.';
END CATCH
```

The divide-by-zero error moves execution to `CATCH`.

</details>

#### 10. If every statement in `TRY` succeeds, SQL Server runs the `CATCH` block. True or False?

<details>

<summary>Solution</summary>

**False.**

`CATCH` runs only when an error occurs in `TRY`.

</details>

#### 11. Write a `TRY...CATCH` block that prints `Calculation completed.` when `100 / 2` runs successfully. Print `Calculation failed.` if an error occurs.

<details>

<summary>Solution</summary>

```sql
BEGIN TRY
    PRINT 100 / 2;
    PRINT 'Calculation completed.';
END TRY
BEGIN CATCH
    PRINT 'Calculation failed.';
END CATCH
```

No error occurs, so the `CATCH` block does not run.

</details>

#### 12. This statement inserts an account with an existing primary key. Write a `TRY...CATCH` block that prints `Account could not be added.` when the insert fails.

```sql
INSERT INTO Accounts (AccountID, AccountHolder, Balance)
VALUES (101, 'Test Account', 5000.00);
```

<details>

<summary>Solution</summary>

```sql
BEGIN TRY
    INSERT INTO Accounts (AccountID, AccountHolder, Balance)
    VALUES (101, 'Test Account', 5000.00);
END TRY
BEGIN CATCH
    PRINT 'Account could not be added.';
END CATCH
```

`AccountID = 101` already exists, so SQL Server enters `CATCH`.

</details>

#### 13. What does this script print?

```sql
BEGIN TRY
    PRINT 50 / 0;
    PRINT 'Done';
END TRY
BEGIN CATCH
    PRINT 'Error handled.';
END CATCH
```

<details>

<summary>Solution</summary>

It prints:

```
Error handled.
```

The divide-by-zero error stops the remaining `TRY` statements. SQL Server then runs `CATCH`.

</details>

### Transactions with exception handling

#### 14. Which action belongs in `CATCH` when a transaction fails?

* A. `COMMIT`
* B. `ROLLBACK`
* C. `BEGIN TRANSACTION`
* D. `INSERT`

<details>

<summary>Solution</summary>

**B. `ROLLBACK`**

It undoes the transaction changes after an error.

</details>

#### 15. Complete the missing command.

```sql
BEGIN TRY
    BEGIN TRANSACTION;

    UPDATE Accounts
    SET Balance = Balance + 250.00
    WHERE AccountID = 104;

    COMMIT;
END TRY
BEGIN CATCH
    ____________;
    PRINT 'Update failed.';
END CATCH
```

<details>

<summary>Solution</summary>

```sql
ROLLBACK;
```

The `CATCH` block undoes transaction changes after an error.

</details>

#### 16. Transfer `3000.00` from Aditi to Kabir. Use `TRY...CATCH`, a transaction, `COMMIT`, `ROLLBACK`, and success or failure messages.

<details>

<summary>Solution</summary>

```sql
BEGIN TRY
    BEGIN TRANSACTION;

    UPDATE Accounts
    SET Balance = Balance - 3000.00
    WHERE AccountID = 101;

    UPDATE Accounts
    SET Balance = Balance + 3000.00
    WHERE AccountID = 104;

    COMMIT;
    PRINT 'Transfer successful.';
END TRY
BEGIN CATCH
    ROLLBACK;
    PRINT 'Transfer failed. Changes were undone.';
END CATCH
```

Both updates commit only when no error occurs.

</details>

#### 17. Start a transaction and add `750.00` to Rohan's balance. Next, insert another row with `AccountID = 102`. Handle the error so Rohan's update is undone. Print a failure message.

<details>

<summary>Solution</summary>

```sql
BEGIN TRY
    BEGIN TRANSACTION;

    UPDATE Accounts
    SET Balance = Balance + 750.00
    WHERE AccountID = 102;

    INSERT INTO Accounts (AccountID, AccountHolder, Balance)
    VALUES (102, 'Duplicate Account', 1000.00);

    COMMIT;
    PRINT 'Transaction completed.';
END TRY
BEGIN CATCH
    ROLLBACK;
    PRINT 'Transaction failed. Changes were undone.';
END CATCH
```

The duplicate primary key causes an error. `ROLLBACK` restores Rohan's original balance.

</details>

#### 18. Write a safe transfer of `500.00` from Kabir to Aditi. The script must display the account rows after it completes successfully.

<details>

<summary>Solution</summary>

```sql
BEGIN TRY
    BEGIN TRANSACTION;

    UPDATE Accounts
    SET Balance = Balance - 500.00
    WHERE AccountID = 104;

    UPDATE Accounts
    SET Balance = Balance + 500.00
    WHERE AccountID = 101;

    COMMIT;
    PRINT 'Transfer successful.';

    SELECT *
    FROM Accounts;
END TRY
BEGIN CATCH
    ROLLBACK;
    PRINT 'Transfer failed. Changes were undone.';
END CATCH
```

The rows are displayed only after a successful commit.

</details>
