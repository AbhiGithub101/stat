---
hidden: true
---

# DBMS and SQL

#### So before we dive into SQL, let us first understand what DBMS are...

## What is a Database?

Before we understand DBMS, let's start with **database**.

A database is just an organised collection of data stored electronically. Think of it like a very well-organised digital filing cabinet. Instead of papers scattered everywhere, every piece of information has its own place,easy to find, easy to update, and easy to delete when no longer needed.

**Example:** A school keeps information about its students ,i.e. names, roll numbers, marks, attendance. If all of this is stored in one organised place where you can search and update instantly, that's a database.

## What is a DBMS?

**DBMS stands for Database Management System.**

It is software that helps you create, store, manage, and retrieve data from a database. You don't interact with the raw data directly , the DBMS sits in the middle and handles everything for you.

Think of it like this:

> **You → DBMS → Database**

You ask for data, the DBMS finds it, gives it to you, updates it, or deletes it — all on your behalf.

**Simple analogy:** Imagine a large library. The library is the database — it holds all the books (data). The librarian is the DBMS — they know where everything is, who can access what, and they make sure books are returned properly. You don't go searching every shelf yourself. You ask the librarian.

### Why Do We Need a DBMS?

Before DBMS systems existed, data was stored in simple files on computers. This caused a lot of problems:

* The same data was stored in multiple places, leading to **duplication and confusion**
* There was **no security** ,anyone could access any file
* Searching or updating data was **slow and error-prone**
* If two people tried to update the same data at the same time, things would **break or conflict**

A DBMS solves all of these problems. It keeps data in one place, controls who can access it, allows multiple users at the same time, and ensures data stays accurate and consistent.

### Types of DBMS

There are a few different types, but don't worry ,we'll mostly focus on one:

**1. Relational DBMS (RDBMS)** :  the most widely used type. Data is stored in tables (rows and columns), and tables can be linked to each other. SQL is the language used to work with this type. Examples: MySQL, PostgreSQL, SQL Server, Oracle.

**2. Non-Relational DBMS** : designed for unstructured data, used in modern apps. Examples: MongoDB, Firebase.

### Where is DBMS Used in Real Life?

DBMS is everywhere ,even if you've never noticed it:

* **Banking** : your account balance, transactions, and loan details are all stored in a database
* **E-commerce:** when you order something on Amazon, a DBMS tracks your order, payment, and delivery
* **Hospitals:** patient records, prescriptions, and doctor schedules are managed through DBMS
* **Airlines** :  seat bookings, passenger details, and flight schedules run on databases
* **Social media** :  every post, like, comment, and follower is stored and retrieved from massive databases

### Quick Summary

| Term     | Meaning                                                  |
| -------- | -------------------------------------------------------- |
| Data     | Raw facts and figures                                    |
| Database | Organised collection of data stored electronically       |
| DBMS     | Software that manages the database                       |
| RDBMS    | A type of DBMS that uses tables — what we'll be learning |
| SQL      | The language used to talk to an RDBMS                    |

### What is SQL?

**SQL stands for Structured Query Language.**

It is the language you use to talk to a relational database. Whenever you want to get data, add new data, update something, or delete something from a database,you do it by writing SQL.

Think of SQL as the language you use to give instructions to your DBMS. The DBMS understands SQL and carries out whatever you ask.

### What is Microsoft SQL Server?

**Microsoft SQL Server is a Relational Database Management System (RDBMS) built by Microsoft.**

It is one of the most widely used database systems in the world, especially in companies that use Windows-based systems and Microsoft technologies. Large businesses, government organisations, hospitals, banks, and many others use SQL Server to store and manage their data.

In simple terms, SQL Server is the software that holds your database, manages it, keeps it secure, and processes all the SQL commands you send to it.

### What is SSMS?

**SSMS stands for SQL Server Management Studio.**

It is a free tool made by Microsoft that gives you a visual interface to connect to SQL Server and work with your databases. Instead of working in a plain black command window, SSMS gives you a proper screen with menus, buttons, and panels ,making it much easier to write SQL, view your tables, manage users, and run queries.

### What Can You Do in SSMS?

SSMS lets you do everything you need as a database user or administrator:

* Connect to a SQL Server (on your own computer or a remote server)
* See all your databases, tables, and their contents visually
* Write and run SQL queries
* Create new databases and tables
* Import and export data
* Manage users and their permissions
* Monitor performance and troubleshoot issues

### How Do SQL, SQL Server, and SSMS Work Together?

| Term       | What It Is        | Simple Description                                           |
| ---------- | ----------------- | ------------------------------------------------------------ |
| SQL        | A language        | The instructions you write to work with data                 |
| SQL Server | A software/engine | The system that stores and manages your databases            |
| SSMS       | A tool/interface  | The screen you use to write SQL and interact with SQL Server |

## Why SQL when we have EXCEL?

1. Excel cannot handle data if there are more than 10lakh rows or 60k columns.
2. Excels starts hanging if data reaches 2lakh or more
3. Excels helps in storing data and performing basic data operations

## What is a table ?

A table is the most fundamental building block of a relational database. It is where all data is actually stored.

A table organises data into **rows and columns** , exactly like a spreadsheet. Each table in a database represents one specific subject or entity, such as customers, employees, products, or orders.

Think of a table like a register that a teacher maintains in school. Each page of that register has columns , Roll Number, Student Name, Class, Marks. And each student occupies one row. That entire register, in database terms, is a table.

### What is Metadata?

The word **metadata** sounds technical, but it is actually a very simple concept once you break it down.

**Meta** means "about." **Data** means "information." So metadata simply means **data about data,** information that describes other information.

Metadata doesn't contain the actual data itself. Instead, it describes the structure, properties, and details of that data.

Think of a book. : The actual content of the book , the story, the chapters, the text ,that is the data. But the cover of the book tells you the title, the author's name, the number of pages, the genre, and the publishing date. None of that is the story itself, but it tells you everything about the book. That information on the cover is metadata.

### Types of SQL

When we talk about "types of SQL," we are talking about the different **categories of SQL commands,**&#x65;ach category designed to do a different kind of job.

SQL has a lot of commands, but every single one of them belongs to one of these groups. Understanding these categories first makes it much easier to learn the individual commands later, because you always know what job a command is meant to do.

There are five main categories. Let's go through each one.

### 1. DDL — Data Definition Language

**DDL commands are used to define and manage the structure of a database.** They deal with creating, modifying, and deleting the objects that hold data , like databases, tables, and columns. DDL is about building and changing the skeleton of your database.

Think of DDL as the construction work. Before you can store anything, you need to build the structure first ,you need to decide what tables exist, what columns they have, and what type of data each column will hold. That's all DDL.

The main DDL commands are:

**CREATE** :  used to create a new database, table, or other object. For example, creating a new table called Employees with columns for ID, Name, and Salary.

**ALTER** : used to modify an existing table. For example, adding a new column to a table, changing a column's data type, or renaming a column.

**DROP** : used to permanently delete an entire table or database. Once you drop something, it is gone  along with all the data inside it.

**TRUNCATE** :  used to remove all the rows from a table at once, but keeps the table structure itself intact. The table still exists, it is just emptied out completely.

### 2. DML - Data Manipulation Language

**DML commands are used to work with the actual data inside the tables.** Once your tables are created using DDL, you use DML to put data in, change it, and remove it. DML is about manipulating the content, not the structure.

This is the category you will use most frequently in day-to-day work. Almost every application , whether it's adding a new customer, updating an address, or deleting a cancelled order , uses DML behind the scenes.

The main DML commands are:

**INSERT** : used to add new rows of data into a table. For example, adding a newly joined employee's details into the Employees table.

**UPDATE** : used to modify existing data in a table. For example, updating a customer's phone number because they changed it.

**DELETE** : used to remove specific rows from a table. For example, deleting an order that was cancelled by the customer.

### 3. DQL - Data Query Language

**DQL is used to retrieve and read data from the database.** It does not change anything ,it simply fetches the data you ask for and displays it to you.

Some people group DQL under DML, but many professionals treat it separately because querying data is such a large and important part of SQL that it deserves its own category.

There is essentially one core DQL command:

**SELECT** : used to fetch data from one or more tables. You can retrieve all data, specific columns, filtered results, sorted results, grouped results, and much more , all using SELECT.

SELECT is by far the most commonly used SQL command. It is the foundation of reporting, dashboards, data analysis, and anything that involves reading data from a database.

### 4. DCL — Data Control Language

**DCL commands are used to control who can access the database and what they are allowed to do.** This is all about security and permissions ,making sure the right people have the right level of access, and everyone else is kept out.

In any real organisation, not everyone should be able to do everything. A junior data analyst might be allowed to read data but not delete it. An HR manager might be allowed to access the HR tables but not the Finance tables. DCL is how these rules are set and enforced.

The main DCL commands are:

**GRANT** : gives a user permission to perform a specific action. For example, giving a user permission to run SELECT queries on the Employees table.

**REVOKE** : takes away a permission that was previously granted. For example, removing someone's ability to delete records after a security concern.

### 5. TCL - Transaction Control Language

**TCL commands are used to manage transactions in a database.** A transaction is a group of SQL operations that are treated as one single unit of work , either all of them succeed together, or none of them go through.

This is extremely important in situations where multiple steps depend on each other. For example, transferring money between two bank accounts involves two steps ,deducting from one account and adding to another. If the first step succeeds but the second one fails due to an error, you can't just leave the data halfway. TCL gives you the control to either confirm all changes or undo them completely.

The main TCL commands are:

**COMMIT** : saves all the changes made during the current transaction permanently to the database. Once you commit, the changes are final.

**ROLLBACK** : undoes all the changes made during the current transaction, taking the database back to its previous state. Used when something goes wrong and you don't want incomplete changes to be saved.

**SAVEPOINT** :  creates a checkpoint within a transaction. If something goes wrong later, you can rollback to the savepoint instead of undoing the entire transaction from the beginning.







