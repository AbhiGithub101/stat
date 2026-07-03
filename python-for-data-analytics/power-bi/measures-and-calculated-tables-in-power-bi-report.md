---
hidden: true
---

# Measures & Calculated Tables In Power BI Report

## What is a Measure in Power BI?

A **Measure** is a **calculation created using DAX (Data Analysis Expressions)** that calculates results **only when needed** based on the data shown in a report.

**Example:**

* Total Sales
* Total Profit
* Average Sales
* Number of Customers
* Maximum Sales
* Minimum Sales
* Growth Percentage
* Profit Margin
* Running Total
* Year-to-Date Sales
* Previous Year Sales



## How to Create Measures&#x20;



<p align="center">Open your report<br>↓<br>Go to the <strong>Modeling</strong> tab<br>↓<br>Click <strong>New Measure</strong><br>↓<br>A formula bar appears<br>↓<br>Write your DAX formula<br>Total Sales = SUM(Sales[Sales Amount])<br>↓<br>Press <strong>Enter</strong><br><strong>(</strong>Your measure appears under the selected table with a calculator icon)</p>





## Benefits of Measures

* Dynamic calculations based on filters and slicers.
* Faster and more memory-efficient than calculated columns.
* Reusable across multiple visuals.
* Ideal for KPIs, totals, averages, percentages, and ratios.
* Automatically updates when report filters change.
* Supports advanced DAX functions like `CALCULATE`, `FILTER`, `ALL`, and `DIVIDE`.











### Difference Between Column and Measure

| Calculated Column               | Measure                                    |
| ------------------------------- | ------------------------------------------ |
| Calculated row by row           | Calculated on demand                       |
| Stored in the model             | Not stored; computed when needed           |
| Increases model size            | Does not increase model size significantly |
| Used for filtering and grouping | Used for aggregations and KPIs             |
| Static after refresh            | Dynamic based on filter context            |







### Calculated Tables in Power BI

#### What is a Calculated Table?

A **Calculated Table** in Power BI is a new table created using **DAX (Data Analysis Expressions)** instead of importing data from an external source. It is stored in the Power BI data model and is **calculated when the data model is refreshed**.



#### When to Use Calculated Tables?

Use calculated tables when you need to:

* Create a Date/Calendar table
* Create summary or aggregated tables
* Combine multiple tables
* Filter existing data into a new table
* Create lookup/reference tables
* Build custom reporting tables





### Difference Between an Imported Table and a Calculated Table

| Imported Table                      | Calculated Table                         |
| ----------------------------------- | ---------------------------------------- |
| Imported from Excel, SQL, CSV, etc. | Created using DAX                        |
| Data comes from external sources    | Data comes from existing Power BI tables |
| Refreshed from the data source      | Recalculated during model refresh        |
| No DAX required                     | Requires DAX formulas                    |
| Can be transformed in Power Query   | Created in the Modeling view             |







### Difference Between Calculated Table, Calculated Column, and Measure

| Feature                | Calculated Table | Calculated Column | Measure                      |
| ---------------------- | ---------------- | ----------------- | ---------------------------- |
| Creates a new table    | ✅                | ❌                 | ❌                            |
| Creates a new column   | ❌                | ✅                 | ❌                            |
| Returns a single value | ❌                | ❌                 | ✅                            |
| Uses DAX               | ✅                | ✅                 | ✅                            |
| Stored in the model    | ✅                | ✅                 | ❌ (calculated at query time) |
| Updates on refresh     | ✅                | ✅                 | Dynamic with filter context  |





## How Measures Work



<p align="center">Data Tables<br>↓<br>Create Measure (DAX Formula)<br>↓<br>Measure calculates values<br>↓<br>Filters/Slicers applied<br>↓<br>Result changes automatically<br>↓<br>Display in Charts, Cards and Tables</p>























































































































































