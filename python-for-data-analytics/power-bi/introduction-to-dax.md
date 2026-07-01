# Introduction to DAX

### What is DAX in Power BI?

**DAX** stands for **Data Analysis Expressions**.

It is a **formula language** used in Power BI to perform calculations and create new information from existing data. It is used to create **calculated columns, measures, and calculated tables** for data analysis.

It works similarly to Excel formulas but is more powerful and is designed for working with large datasets.

<p align="center"><strong>DAX</strong> → Performs calculations after data is loaded.</p>

<p align="center"></p>

### Why is DAX Used?

DAX is used to:

* Calculate **Total Sales**.
* Find **Average Sales**.
* Calculate **Profit** and **Profit Percentage**.
* Compare **Current Year Sales** with **Previous Year Sales**.
* Create **Year-to-Date (YTD)** and **Month-to-Date (MTD)** calculations.
* Create **Rankings** of products or customers.
* Apply Logical conditions such as **IF**, **AND**, and **OR**.
* Create **Calculated Columns**, **Measures**, and **Calculated Tables**.



#### How DAX Works



1. **Functions + Operators + Values** — DAX formulas combine built-in functions (like SUM, CALCULATE) with column references, operators, and constants.<br>
2. **Row Context vs Filter Context** — This is DAX's core engine concept:

* _Row context_ = evaluates a formula one row at a time (used in calculated columns).
* _Filter context_ = the set of filters applied by slicers, visuals, or CALCULATE (used in measures).<br>

3. **Evaluation** — When a visual is rendered, Power BI applies the current filter context, then runs the DAX formula against the data model to produce a single value.<br>
4. **Relationships matter** — DAX formulas often pull data across related tables using the model's relationships (e.g., RELATED, RELATEDTABLE).





#### Most-Used DAX Formulas (with Examples)

**1. SUM** — adds up a column

```
Total Sales = SUM(Sales[SalesAmount])
```

**2. AVERAGE** — calculates mean value

```
Avg Order Value = AVERAGE(Sales[SalesAmount])
```

**3. COUNTROWS** — counts rows in a table

```
Total Orders = COUNTROWS(Sales)
```

**4. DISTINCTCOUNT** — counts unique values

```
Unique Customers = DISTINCTCOUNT(Sales[CustomerID])
```

**5. CALCULATE** — changes filter context (most important function in DAX)

```
Sales 2025 = CALCULATE(SUM(Sales[SalesAmount]), Sales[Year] = 2025)
```

**6. FILTER** — returns a filtered table for use inside other functions

```
High Value Sales = CALCULATE(SUM(Sales[SalesAmount]), FILTER(Sales, Sales[SalesAmount] > 1000))
```

**7. ALL** — removes filters from a column/table

```
% of Total Sales = DIVIDE(SUM(Sales[SalesAmount]), CALCULATE(SUM(Sales[SalesAmount]), ALL(Sales)))
```

**8. RELATED** — pulls a value from a related table

```
Product Category = RELATED(Product[Category])
```

**9. SUMX** — row-by-row sum with an expression (iterator)

```
Total Revenue = SUMX(Sales, Sales[Quantity] * Sales[UnitPrice])
```

**10. IF** — conditional logic

```
Sales Status = IF(SUM(Sales[SalesAmount]) > 10000, "High", "Low")
```

**11. SWITCH** — multiple conditions (cleaner than nested IFs)

```
Sales Tier = SWITCH(TRUE(),
    Sales[Amount] > 50000, "Platinum",
    Sales[Amount] > 20000, "Gold",
    Sales[Amount] > 5000, "Silver",
    "Bronze")
```

**12. DIVIDE** — safe division (auto-handles divide-by-zero)

```
Profit Margin = DIVIDE(SUM(Sales[Profit]), SUM(Sales[SalesAmount]), 0)
```

**13. TOTALYTD** — year-to-date total (time intelligence)

```
YTD Sales = TOTALYTD(SUM(Sales[SalesAmount]), 'Date'[Date])
```

**14. DATEADD** — shifts dates for comparison periods

```
Sales Last Year = CALCULATE(SUM(Sales[SalesAmount]), DATEADD('Date'[Date], -1, YEAR))
```

**15. SAMEPERIODLASTYEAR** — compares to same period last year

```
Sales PY = CALCULATE(SUM(Sales[SalesAmount]), SAMEPERIODLASTYEAR('Date'[Date]))
```

**16. RANKX** — ranks values

```
Product Rank = RANKX(ALL(Product[ProductName]), SUM(Sales[SalesAmount]))
```

**17. VAR / RETURN** — stores intermediate values for cleaner, faster formulas

```
Profit % =
VAR TotalSales = SUM(Sales[SalesAmount])
VAR TotalCost = SUM(Sales[Cost])
RETURN DIVIDE(TotalSales - TotalCost, TotalSales)
```

**18. CONCATENATE / &** — joins text

```
Full Name = Customer[FirstName] & " " & Customer[LastName]
```

```
Full Name = Customer[FirstName] & "_" & Customer[LastName]
```

```
Full Name = Customer[FirstName] & "." & Customer[LastName]
```

















































































































































































