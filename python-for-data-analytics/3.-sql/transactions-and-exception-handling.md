# Transactions and Exception Handling

## What is a Transaction?

A Transaction is a **group of SQL statements that are treated as one single unit.** Either ALL of them succeed together or NONE of them happen at all.

Think of it like this:

You are transferring ₹5000 from your account to your friend's account :

* **Step 1** :  Deduct ₹5000 from your account
* **Step 2** : Add ₹5000 to your friend's account

Both steps must happen together. If Step 1 happens but Step 2 fails ,money is gone from your account but never reached your friend. That is a disaster.

A transaction makes sure **either both steps happen or neither happens.**

#### Visual Diagram  Without Transaction:

```
Without Transaction:

  Step 1: Deduct ₹5000        Step 2: Add ₹5000
  from Your Account           to Friend's Account
  ┌─────────────────┐         ┌─────────────────┐
  │ Your Balance:   │         │ Friend Balance: │
  │ ₹10000 → ₹5000  │         │ ₹2000 → ???     │
  │    Done         │  ERROR  │ ❌ Failed        │
  └─────────────────┘         └─────────────────┘
          ↓
  ₹5000 deducted from
  your account but never
  reached friend!
  Money is LOST!
```

#### Visual Diagram With Transaction:

```
With Transaction:

  Step 1: Deduct ₹5000        Step 2: Add ₹5000
  from Your Account           to Friend's Account
  ┌─────────────────┐         ┌─────────────────┐
  │ Your Balance:   │         │ Friend Balance: │
  │ ₹10000 → ₹5000  │         │ ₹2000 → ???     │
  │    Done         │  ERROR  │ ❌ Failed        │
  └─────────────────┘         └─────────────────┘
          ↓
  Transaction sees the error
          ↓
  ROLLBACK! Undo everything!
          ↓
  ┌─────────────────┐         ┌─────────────────┐
  │ Your Balance:   │         │ Friend Balance: │
  │ Back to ₹10000  │         │ Still ₹2000     │
  │    Safe!        │         │    Safe!        │
  └─────────────────┘         └─────────────────┘
  Everything went back
  to original state!
```

#### Transaction Commands

| Command             | What it does                             |
| ------------------- | ---------------------------------------- |
| `BEGIN TRANSACTION` | Marks the start of a transaction         |
| `COMMIT`            | Saves all changes permanently            |
| `ROLLBACK`          | Undoes all changes back to the beginning |

#### 1. BEGIN TRANSACTION & COMMIT

**COMMIT** means everything went well, **save all changes permanently.**

**Syntax:**

```sql
BEGIN TRANSACTION;

    -- your SQL statements here

COMMIT;
```

**Example -> Transfer money:**

```sql
BEGIN TRANSACTION;

    UPDATE Accounts SET Balance = Balance - 5000 WHERE AccountID = 1;
    UPDATE Accounts SET Balance = Balance + 5000 WHERE AccountID = 2;

COMMIT;
```

**Visual:**

```
BEGIN TRANSACTION
        ↓
  Step 1: Deduct ₹5000 
        ↓
  Step 2: Add ₹5000 
        ↓
     COMMIT
        ↓
  Changes saved permanently 
```

> Both steps succeeded ,COMMIT saves everything permanently. Done

#### 2. ROLLBACK ( Undo Everything )

**ROLLBACK** means something went wrong, **undo all changes** back to where the transaction started.

**Syntax:**

```sql
BEGIN TRANSACTION;

    -- your SQL statements here

ROLLBACK;
```

**Example:**

```sql
BEGIN TRANSACTION;

    UPDATE Accounts SET Balance = Balance - 5000 WHERE AccountID = 1;
    -- Imagine something goes wrong here
    UPDATE Accounts SET Balance = Balance + 5000 WHERE AccountID = 99; -- Wrong ID

ROLLBACK; -- Undo everything
```

**Visual:**

```
BEGIN TRANSACTION
        ↓
  Step 1: Deduct ₹5000 
        ↓
  Step 2: Add ₹5000 ❌ (Wrong ID — failed)
        ↓
     ROLLBACK
        ↓
  Step 1 is also undone 
        ↓
  Everything back to
    original state 
```

> ROLLBACK cancelled Step 1 as well , even though it succeeded because Step 2 failed. This is the power of transactions.

#### COMMIT vs ROLLBACK -> Side by Side

```
BEGIN TRANSACTION
        ↓
   All steps run
        ↓
┌───────────────────────┐
│  Everything OK?       │──► COMMIT ──► Changes saved permanently
│  Something wrong? ❌   │──► ROLLBACK ──► Everything undone
└───────────────────────┘
```

## EXCEPTION HANDLING

Exception handling means **catching errors gracefully** instead of letting SQL crash and show a confusing error message, you catch the error and handle it properly.

Think of it like this: You are driving a car  and a tyre bursts. Without exception handling ,the car crashes. With exception handling ,the car safely pulls over and shows you a proper message saying "Tyre puncture,please fix."

#### TRY...CATCH in SQL Server

SQL Server uses **TRY...CATCH** for exception handling:

* **TRY block** → write your SQL code here ,the code you want to run
* **CATCH block** → if anything goes wrong in TRY,execution jumps here automatically

**Visual Diagram:**

```
┌─────────────────────────┐
│        TRY Block        │
│                         │
│  Your SQL code runs     │
│  here normally          │
│                         │
│  If no error ──────────►│──► Continues normally 
│  If error occurs        │
└────────────┬────────────┘
             │ Error!
             ▼
┌─────────────────────────┐
│       CATCH Block       │
│                         │
│  Jumps here when error  │
│  happens automatically  │
│                         │
│  Show error message     │
│  Do ROLLBACK            │
│  Log the error etc.     │
└─────────────────────────┘
```

**Syntax:**

```sql
BEGIN TRY
    -- SQL code you want to run
END TRY
BEGIN CATCH
    -- What to do when error occurs
    -- Show error, rollback, log etc.
END CATCH
```

**Example 1 :** **Simple TRY...CATCH:**

```sql
BEGIN TRY
    PRINT 100 / 0; -- This causes divide by zero error!
END TRY
BEGIN CATCH
    PRINT 'Oops! An error occurred.';
END CATCH
```

**Result:**

```
Oops! An error occurred.
```

> Without TRY...CATCH ,SQL would crash with a red error. With TRY...CATCH,we caught it and showed a clean message.

#### Combining TRY...CATCH with Transactions

This is the **most important and most used pattern** in real SQL projects ,TRY...CATCH wrapped around a transaction:

* If everything works → COMMIT
* If anything fails → ROLLBACK + show error

**Syntax:**

```sql
BEGIN TRY
    BEGIN TRANSACTION;

        -- your SQL statements

    COMMIT;
    PRINT 'Transaction completed successfully!';
END TRY
BEGIN CATCH
    ROLLBACK;
    PRINT 'Something went wrong! Changes have been undone.';
END CATCH
```

**Example -> Safe Money Transfer:**

```sql
BEGIN TRY
    BEGIN TRANSACTION;

        -- Deduct from Account 1
        UPDATE Accounts
        SET Balance = Balance - 5000
        WHERE AccountID = 1;

        -- Add to Account 2
        UPDATE Accounts
        SET Balance = Balance + 5000
        WHERE AccountID = 2;

    COMMIT;
    PRINT 'Transfer successful!';

END TRY
BEGIN CATCH
    ROLLBACK;
    PRINT 'Transfer failed! Amount has been reversed. ❌';
END CATCH
```

**Visual:**

```
BEGIN TRY
        ↓
  BEGIN TRANSACTION
        ↓
  Deduct ₹5000 
        ↓
  Add ₹5000
        ↓
  ┌─────────────────────────────────┐
  │ Success?                        │──► COMMIT ──► 'Transfer successful!'
  │ Error? ❌                        │──► goes to CATCH
  └─────────────────────────────────┘
        ↓ (if error)
  END TRY ──► BEGIN CATCH
        ↓
  ROLLBACK 
        ↓
  'Transfer failed! Amount reversed'
  + Error message shown
  END CATCH
```

**Example :** **Safe Employee Insert:**

```sql
BEGIN TRY
    BEGIN TRANSACTION;

        INSERT INTO Employee VALUES (1, 'Rahul Sharma', 50000);
        -- ID 1 already exists — PRIMARY KEY error!

    COMMIT;
    PRINT 'Employee added successfully!';

END TRY
BEGIN CATCH
    ROLLBACK;
    PRINT 'Failed to add employee! No changes were made.';
END CATCH
```

**Result:**

```
Failed to add employee! No changes were made.
```

> The insert failed,ROLLBACK made sure nothing was partially saved. Clean and safe.



> **Up Next:** Next module we cover **Subqueries and Scalar Functions** ,how to write a query inside another query and how to create your own custom functions that return a single value.

