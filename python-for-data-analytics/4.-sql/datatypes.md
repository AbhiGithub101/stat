---
hidden: true
---

# Datatypes

## What is a Data Type?

When you create a table in SQL, every column needs a **data type** - it tells SQL _what kind of data_ will go in that column.

```mermaid
graph TD
  Datatype --> Numeric
  Numeric --> Exact
  Numeric --> Approximate
  Datatype --> Character/String
  Character/String --> Non-Unicode
  Character/String --> Unicode
  Datatype-->Datetime
  
   
  
```

## 1. Numeric Data Types

Used when you want to store **numbers** like age, price, marks, quantity, etc.

Numeric types are split into two groups:

a. Exact Numeric Types

b. Approximate Numeric Types

### A) Exact Numeric Types

These store numbers **exactly as they are** ,no rounding, no approximation. we use these when accuracy matters (like money).

| Data Type       | What it stores               | Range                               | Real-life Example                                     |
| --------------- | ---------------------------- | ----------------------------------- | ----------------------------------------------------- |
| `INT`           | Whole numbers (no decimals)  | -2,147,483,648 to 2,147,483,647     | Student roll number, age                              |
| `BIGINT`        | Very large whole numbers     | -9.2 quintillion to 9.2 quintillion | Population of the world, bank transaction IDs         |
| `SMALLINT`      | Small whole numbers          | -32,768 to 32,767                   | Number of students in a class                         |
| `TINYINT`       | Very small whole numbers     | 0 to 255                            | Star rating (1–5), floor number                       |
| `DECIMAL(p,s)`  | Numbers with decimals, exact | Depends on precision you set        | <p>Product price ₹199.99, </p><p>exam score 95.50</p> |

> **p stands for precision and s stands for scale**
>
> **p** = total digits (before + after decimal)
>
> **s** = digits after decimal point&#x20;
>
> Example:&#x20;
>
> ### `DECIMAL(5,2)`
>
> * Total digits = 5
> * Decimal digits = 2
> * Before decimal = 5 - 2 = 3
>
> Allowed values:
>
> * `123.45`&#x20;
> * `1.23`&#x20;
> * `999.99`  (max)
>
> Not allowed:
>
> * `1234.56` (4 digits before decimal → exceeds limit)

<img src="../../.gitbook/assets/file.excalidraw (1) (1).svg" alt="" class="gitbook-drawing">

**Simple Example:**

```sql
-- Storing a student's details
RollNo   INT         → 101
Age      TINYINT     → 17
Fees     DECIMAL(8,2) → 45000.00
```

### B) Approximate Numeric Types

These store numbers with **very large or very small values**, but they may be slightly rounded. Used in science,engineering not for money.

| Data Type | What it stores                      | Range                        | Real-life Example                                 |
| --------- | ----------------------------------- | ---------------------------- | ------------------------------------------------- |
| `FLOAT`   | Large decimal numbers (approximate) | Up to 15 digits of precision | Distance between planets, scientific measurements |
| `REAL`    | Similar to FLOAT but smaller        | Up to 7 digits of precision  | Temperature readings, sensor data                 |

**Simple Example:**

```sql
Temperature   REAL     → 36.6
Distance      FLOAT    → 149600000.5  (distance from Earth to Sun in km)
```

> &#x20;**Important:** Never use FLOAT/REAL for money — because 10.10 might get stored as 10.09999... due to approximation. Always use DECIMAL for prices.

### 2.  Character / String Data Types

Used when you want to store **text**  like names, addresses, emails, descriptions, etc.

Character / String Data Types are split into two groups:

A) Non-Unicode (Regular Characters)

B) Unicode (Multi-language Characters)

#### A) Non-Unicode (Regular Characters)

Stores normal **English letters and common symbols** only. Takes **1 byte per character**.

| Data Type    | What it stores                                                                    | Max Size         | Real-life Example                            |
| ------------ | --------------------------------------------------------------------------------- | ---------------- | -------------------------------------------- |
| `CHAR(n)`    | Fixed-length text. Always uses exactly n characters (pads with spaces if shorter) | 8,000 characters | Gender field: 'M' or 'F', Country code: 'IN' |
| `VARCHAR(n)` | Variable-length text. Only uses as much space as needed                           | 8,000 characters | Student name, email address                  |
| `TEXT`       | Very long text                                                                    | Up to 2 GB       | Article content, product description         |

**CHAR vs VARCHAR :**

Imagine you have a box:

* `CHAR(10)` always gives you a box of size 10, even if you put only 3 items. The rest is empty space.
* `VARCHAR(10)` gives you a box that shrinks to fit only what you put in.

sql

```sql
-- If you store 'Ram' in CHAR(10)   → stored as 'Ram       ' (7 spaces added)
-- If you store 'Ram' in VARCHAR(10) → stored as 'Ram' (no extra space)
```

**Simple Example:**

```sql
StudentName   VARCHAR(50)  → 'Rahul Sharma'
Gender        CHAR(1)      → 'M'
Address       VARCHAR(255) → '12, MG Road, Kanpur'
```

#### B) Unicode (Multi-language Characters)

Stores text from **any language** - Hindi, Arabic, Chinese, Japanese, emojis, etc. Takes **2 bytes per character**.

| Data Type     | What it stores               | Max Size         | Real-life Example                      |
| ------------- | ---------------------------- | ---------------- | -------------------------------------- |
| `NCHAR(n)`    | Fixed-length Unicode text    | 4,000 characters | Fixed-length code in any language      |
| `NVARCHAR(n)` | Variable-length Unicode text | 4,000 characters | Name in Hindi, Arabic, or any language |
| `NTEXT`       | Very long Unicode text       | Up to 2 GB       | Multilingual article or content        |

> The **"N"** in front stands for **National** (language support).

**Simple Example:**

> ```sql
> StudentName   NVARCHAR(50)  → N'राहुल शर्मा'-- Hindi name
> CityName      NVARCHAR(100) → N'東京'    -- Tokyo in Japanese
> ```

### 3. Date and Time Data Types

Used to store **dates, times, or both** - like date of birth, order time, joining date, etc.

| Data Type       | What it stores             | Range                    | Real-life Example                                     |
| --------------- | -------------------------- | ------------------------ | ----------------------------------------------------- |
| `DATE`          | Only date (no time)        | 0001-01-01 to 9999-12-31 | Date of birth, joining date                           |
| `TIME`          | Only time (no date)        | 00:00:00 to 23:59:59.999 | Class timing, shop opening time                       |
| `DATETIME`      | Both date and time         | 1753-01-01 to 9999-12-31 | Order placed timestamp, login time                    |
| `DATETIME2`     | More precise date + time   | 0001-01-01 to 9999-12-31 | More accurate than DATETIME, preferred in new systems |
| `SMALLDATETIME` | Date + time (less precise) | 1900-01-01 to 2079-06-06 | When you don't need high precision                    |

**Simple Example:**

```sql
DateOfBirth     DATE          → 2005-08-15
ClassStartTime  TIME          → 09:30:00
OrderPlacedAt   DATETIME      → 2024-03-25 14:45:30
```

**Real-life scenario - Online Order Table:**

```sql
OrderID        INT              → 5001
CustomerName   VARCHAR(100)     → 'Priya Verma'
OrderAmount    DECIMAL(10,2)    → 1299.99
OrderDate      DATETIME         → 2024-03-25 10:30:00
DeliveryDate   DATE             → 2024-03-28
```

### 4. BIT Data Type

| Data Type | What it stores                  | Range          | Real-life Example                           |
| --------- | ------------------------------- | -------------- | ------------------------------------------- |
| `BIT`     | Only two values - true or false | 0, 1 (or NULL) | Is a student active? Is an order delivered? |

Think of it like a **light switch** -it's either ON (1) or OFF (0).

```sql
IsActive       BIT  → 1   (means Yes / True)
IsDelivered    BIT  → 0   (means No / False)
```

## Additional / Special Data Types

### 1. UUID & GUID

#### A. UUID&#x20;

**UUID** stands for **Universally Unique Identifier.** It is a **very long, auto-generated code** that is guaranteed to be unique across the entire world ,no two systems will ever generate the same UUID.

**Real-life example:** When you sign up on an app, instead of giving you Roll No. 1, 2, 3... the system gives you a unique ID like the one above so that even if millions of users sign up across different servers, no two users will ever get the same ID.

It looks like this:

```
550e8400-e29b-41d4-a716-446655440000
```

It has 32 characters + 4 hyphens split into 5 groups.

### B. GUID

**GUID** stands for **Globally Unique Identifier.**

> GUID and UUID are essentially **the same thing.** UUID is the universal standard term, and GUID is what **Microsoft / SQL Server calls it.**
>
>

### UNIQUEIDENTIFIER — The Data Type in SQL Server

In SQL Server, the data type used to store a UUID / GUID is called `UNIQUEIDENTIFIER`:

```sql
-- Creating a column with UNIQUEIDENTIFIER
CREATE TABLE Employee (
    ID        UNIQUEIDENTIFIER PRIMARY KEY,
    FullName  VARCHAR(100)
);
```

You can auto-generate a GUID in SQL Server using `NEWID()`:

```sql
INSERT INTO Employee VALUES (NEWID(), 'Rahul Sharma');
INSERT INTO Employee VALUES (NEWID(), 'Priya Verma');
```

**What the table looks like:**

| ID                                   | FullName     |
| ------------------------------------ | ------------ |
| 7D9F2A1B-3C4E-4F8A-B123-9E0D6C7A8B5F | Rahul Sharma |
| A1B2C3D4-E5F6-7890-ABCD-EF1234567890 | Priya Verma  |

> Every time `NEWID()` runs it generates a completely new and unique value — no two will ever be the same.

#### UUID vs GUID — One Line Difference

| Term | Used By                                                     |
| ---- | ----------------------------------------------------------- |
| UUID | Universal standard — MySQL, PostgreSQL, general programming |
| GUID | Microsoft's name for the same thing — SQL Server            |

> &#x20;Same concept, different names depending on which database you are using.

#### INT vs UNIQUEIDENTIFIER — Which one to use?

|                        | INT                          | UNIQUEIDENTIFIER                |
| ---------------------- | ---------------------------- | ------------------------------- |
| Looks like             | 1, 2, 3, 4...                | 7D9F2A1B-3C4E-4F8A-...          |
| Easy to read?          | Yes                          |  Not really                     |
| Unique across servers? |  No                          |  Yes                            |
| Use when               | Single database, simple apps | Large systems, multiple servers |

### 2.  XML Data Type

#### What is XML?

**XML** stands for **Extensible Markup Language.** It is a way of storing data in a **tag-based format,**&#x73;imilar to how HTML looks.

It looks like this:

```xml
<Employee>
    <Name>Rahul Sharma</Name>
    <Department>IT</Department>
    <Salary>50000</Salary>
</Employee>
```

#### XML in SQL Server

SQL Server has a built-in `XML` data type that lets you store XML data directly inside a column:

| Data Type | What it stores     | Max Size   | Real-life Example                               |
| --------- | ------------------ | ---------- | ----------------------------------------------- |
| `XML`     | XML formatted data | Up to 2 GB | Config settings, product details, API responses |

```sql
CREATE TABLE EmployeeDetails (
    ID       INT PRIMARY KEY,
    FullName VARCHAR(100),
    ExtraInfo XML
);
```

```sql
INSERT INTO EmployeeDetails VALUES (
    1,
    'Rahul Sharma',
    '<Info><Skill>SQL</Skill><Skill>Python</Skill><City>Kanpur</City></Info>'
);
```

**What the table looks like:**

**What the table looks like:**

| ID | FullName     | ExtraInfo                                                                 |
| -- | ------------ | ------------------------------------------------------------------------- |
| 1  | Rahul Sharma | `<Info><Skill>SQL</Skill><Skill>Python</Skill><City>Kanpur</City></Info>` |

**Real-life example:** When a company receives data from an outside system or API in XML format , they can store it directly in an XML column without breaking it apart.

> XML is useful when the data does not fit neatly into fixed columns , like a product that has different attributes depending on its category.

### 3.  Binary Data Types

#### What is Binary Data?

Binary data means **files and raw data**  like images, PDFs, audio files, Word documents, fingerprints, etc. These are not text or numbers , they are stored as **raw bytes (0s and 1s).**

SQL Server has these binary data types:

| Data Type        | What it stores              | Max Size    | Real-life Example                    |
| ---------------- | --------------------------- | ----------- | ------------------------------------ |
| `BINARY(n)`      | Fixed-length binary data    | 8,000 bytes | Fixed size raw data, encryption keys |
| `VARBINARY(n)`   | Variable-length binary data | 8,000 bytes | Small images, small files            |
| `VARBINARY(MAX)` | Very large binary data      | Up to 2 GB  | Profile photos, PDFs, documents      |

#### BINARY vs VARBINARY - Same as CHAR vs VARCHAR

Just like we saw earlier:

* `BINARY(n)` — always takes fixed space, even if data is smaller
* `VARBINARY(n)` — takes only as much space as the data needs

#### Simple Example

```sql
CREATE TABLE EmployeeFiles (
    ID            INT PRIMARY KEY,
    FullName      VARCHAR(100),
    ProfilePhoto  VARBINARY(MAX),
    Fingerprint   BINARY(64)
);
```

**Real-life examples of binary data in databases:**

| Scenario                         | Data Type to use |
| -------------------------------- | ---------------- |
| Storing a profile photo          | `VARBINARY(MAX)` |
| Storing a scanned document / PDF | `VARBINARY(MAX)` |
| Storing a fingerprint scan       | `BINARY(64)`     |
| Storing an encryption key        | `BINARY(32)`     |

> &#x20;In most real projects, instead of storing the actual file in the database, developers store the **file path** (like `'images/rahul.jpg'`) as a VARCHAR — and keep the actual file on the server. But when security is important — like fingerprints or encrypted data — binary is stored directly in the database.

| Data Type          | Use When                                     |
| ------------------ | -------------------------------------------- |
| `UNIQUEIDENTIFIER` | You need a globally unique ID across systems |
| `XML`              | You need to store tag-based structured data  |
| `BINARY(n)`        | Fixed-size raw data like encryption keys     |
| `VARBINARY(n)`     | Variable-size raw data like small files      |
| `VARBINARY(MAX)`   | Large files like photos, PDFs, documents     |
