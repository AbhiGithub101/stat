# Report View, Table View and Model View

In **Power BI Desktop**, there are **3 main views**:

* **Report View**
* **Table View** or **Data View**
* **Model View**

Each view has a different job.

* **Report View** is used to create charts and dashboards.
* **Table View** is used to inspect data row by row.
* **Model View** is used to connect tables.

If you are new to BI, remember this order:

1. Check the data.
2. Connect the tables.
3. Build the report.

### Report View

**Report View** is where you build charts and dashboards.

You use it to:

* create visuals
* compare values
* find trends
* present business insights clearly

<figure><img src="../../.gitbook/assets/Dashboard (1).png" alt=""><figcaption></figcaption></figure>

### Table View or Data View

**Table View** shows the actual data inside each table.

You use it to:

* inspect rows and columns
* verify values
* check data types
* create calculated columns

This view helps you confirm that the data is correct before building visuals.

<figure><img src="../../.gitbook/assets/Table view.png" alt=""><figcaption></figcaption></figure>

### Model View

**Model View** shows the relationships between different tables in the Power BI data model.

#### Why it is important

* Create relationships between tables.
* Manage star and snowflake schemas.
* Define cardinality like `1:*` and `*:1`.
* Improve report logic and performance.

<figure><img src="../../.gitbook/assets/Model_vv.jpg" alt=""><figcaption></figcaption></figure>

After data is loaded, Power BI may create some relationships automatically. You should still check them manually. Make sure the correct columns are connected. You can also delete wrong relationships.

You can also create relationships manually in two ways:

* Drag and Drop
* Manage Relationships

1. **Drag and Drop** creates a relationship by connecting a common column from one table to the matching column in another table.

* Quickly create relationships.
* Connect fact and dimension tables.
* Enable filtering across tables.

<figure><img src="../../.gitbook/assets/Drag and Drop.png" alt=""><figcaption></figcaption></figure>

#### Example

Suppose you have:

**Sales Table**

* Customer\_ID
* Product\_ID
* Sales\_Amount

**Customer Table**

* Customer\_ID
* Customer\_Name

You can drag **Customer\_ID** from the Sales table to **Customer\_ID** in the Customer table. This creates a relationship between both tables.

<figure><img src="../../.gitbook/assets/DD_pb.png" alt=""><figcaption></figcaption></figure>

2. **Manage Relationships** lets you create, edit, delete, and view relationships manually.

* Create relationships when Power BI does not detect them automatically.
* Modify existing relationships.
* Set cardinality.
* Configure cross filter direction.

<figure><img src="../../.gitbook/assets/Manage_Rel.png" alt=""><figcaption></figcaption></figure>

<p align="center"><strong>Click on Manage Relationships ------> Select New Relationships</strong></p>

<figure><img src="../../.gitbook/assets/NR_relation.png" alt=""><figcaption></figcaption></figure>

In this example, **FactSale** is connected to **DimDate** by the date column. This is a **Many-to-One (`*:1`)** relationship. Many sales rows can match one date row.

The cross filter direction is **Single**. This means the Date table can filter the Sales table. This helps with monthly, quarterly, and yearly analysis.

<figure><img src="../../.gitbook/assets/Edit_relation.png" alt=""><figcaption></figcaption></figure>

### Types of tables

In Power BI, the two main table types are:

1. Fact Table
2. Dimension Table

#### 1. Fact Table

A **Fact Table** stores measurable business data.

**Main points:**

* It stores numeric values such as Sales, Profit, Quantity, and Cost.
* It usually has many rows.
* It contains keys that connect to dimension tables.
* It represents transactions or business events.

**Example:** Sales Fact Table

| OrderID | ProductID | CustomerID | DateID | SalesAmount | Quantity |
| ------- | --------- | ---------- | ------ | ----------- | -------- |
| 101     | P01       | C01        | D01    | 5000        | 2        |
| 102     | P02       | C02        | D02    | 3000        | 1        |

Here, **SalesAmount** and **Quantity** are the facts.

#### 2. Dimension Table

A **Dimension Table** stores descriptive information about the business.

Examples include product, customer, date, city, and region data.

**Main points:**

* It contains text or descriptive columns.
* It usually has fewer rows than a fact table.
* It is used for filtering, grouping, and slicing.
* It connects to fact tables.

**Example:** Product Dimension Table

| ProductID | ProductName          | Category    |
| --------- | -------------------- | ----------- |
| P01       | ConsoleFlare\_Laptop | Electronics |
| P02       | ConsoleFlare\_Mobile | Electronics |

**Example:** Customer Dimension Table

| CustomerID | CustomerName    | City   |
| ---------- | --------------- | ------ |
| C01        | ConsoleFlare\_A | Delhi  |
| C02        | ConsoleFlare\_B | Mumbai |

### Types of relationships between tables

In Power BI, there are 4 main relationship types.

| Relationship Type | Symbol | Simple meaning                               |
| ----------------- | ------ | -------------------------------------------- |
| **One-to-One**    | `1:1`  | One row matches one row.                     |
| **One-to-Many**   | `1:*`  | One row matches many rows.                   |
| **Many-to-One**   | `*:1`  | Many rows match one row.                     |
| **Many-to-Many**  | `*:*`  | Many rows in both tables can match together. |

### 1. One-to-One Relationship (`1:1`)

Each record in one table matches only one record in another table.

**Example:**

**Employee Table**

| EmployeeID | Name            | City   | Area  |
| ---------- | --------------- | ------ | ----- |
| 101        | ConsoleFlare\_1 | Mumbai | Dadar |
| 102        | ConsoleFlare\_2 | Pune   | Baner |

**Salary Table**

| EmployeeID | Salary | Provident\_Fund | Years\_of\_Experence |
| ---------- | ------ | --------------- | -------------------- |
| 101        | 50,000 | 4800            | 5                    |
| 102        | 60,000 | 5600            | 7                    |

* Employee **101** has one salary record.
* Employee **102** has one salary record.

**Use case:** Employee details ↔ Employee salary

This relationship is less common in Power BI.

<figure><img src="../../.gitbook/assets/r_1.png" alt=""><figcaption></figcaption></figure>

### 2. One-to-Many Relationship (`1:*`)

One record in the first table can match many records in the second table.

**Example:**

**Customer Table**

| CustomerID | CustomerName |
| ---------- | ------------ |
| C01        | Rahul        |
| C02        | Priya        |

**Orders Table**

| OrderID | CustomerID | Amount |
| ------- | ---------- | ------ |
| O101    | C01        | 1000   |
| O102    | C01        | 1500   |
| O103    | C02        | 2000   |

* Customer **C01** has multiple orders.
* Customer **C02** has one order.

**Use case:** Customer → Orders

This is the most common relationship in Power BI.

<figure><img src="../../.gitbook/assets/Screenshot 2026-06-13 170017.png" alt=""><figcaption></figcaption></figure>

### 3. Many-to-One Relationship (`*:1`)

Many records in the first table match one record in the second table.

**Example:**

**Sales Table**

| ProductID | Quantity |
| --------- | -------- |
| P01       | 5        |
| P01       | 8        |
| P02       | 10       |

**Product Table**

| ProductID | ProductName |
| --------- | ----------- |
| P01       | Laptop      |
| P02       | Mobile      |

* Many sales records belong to one product.

**Use case:** Sales → Product

<figure><img src="../../.gitbook/assets/Screenshot 2026-06-13 170017.png" alt=""><figcaption></figcaption></figure>

### 4. Many-to-Many Relationship (`*:*`)

Many records in both tables can be related to each other.

**Example:**

**Student Table**

| StudentID | StudentName |
| --------- | ----------- |
| S01       | Rahul       |
| S02       | Priya       |

**Course Table**

| CourseID | CourseName |
| -------- | ---------- |
| C01      | Python     |
| C02      | SQL        |

**Enrollment Table**

| StudentID | CourseID |
| --------- | -------- |
| S01       | C01      |
| S01       | C02      |
| S02       | C01      |

* Rahul can enroll in many courses.
* Python course can have many students.

**Use case:** Students ↔ Courses

<figure><img src="../../.gitbook/assets/Screenshot 2026-06-13 171810.png" alt=""><figcaption></figcaption></figure>

### Common visuals used in Report View

In Report View, charts help you analyse data visually. They make it easier to compare values, find patterns, and explain results.

The most commonly used visuals are:

1. **Table Visual** – To verify imported data.
2. **Matrix Visual** – To analyze relationships between dimensions and facts.
3. **Bar/Column Chart** – To compare measures across categories.
4. **Line Chart** – To analyze trends over time.
5. **Scatter Chart** – To study correlations between variables.
6. **Treemap** – To analyze hierarchical data.
7. **Decomposition Tree** – To drill down into measures and dimensions.
