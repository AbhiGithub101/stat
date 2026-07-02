---
hidden: true
---

# Measures & Calculated Tables In Power BI Report

## What is a Measure in Power BI?

A **Measure** is a DAX (Data Analysis Expressions) formula that performs calculations on your data. Unlike calculated columns, measures are calculated **only when they are used in a visual**.

**Example:**

* Total Revenue
* Total Profit
* Average Sales
* Profit Margin
* Total Quantity









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





























































































































































