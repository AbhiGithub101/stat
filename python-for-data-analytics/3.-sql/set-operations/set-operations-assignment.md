---
description: Practice UNION, UNION ALL, INTERSECT, and EXCEPT in SQL Server.
---

# Set Operations Assignment

### Practice dataset

```sql
CREATE TABLE OnlineOrders (
    OrderID INT,
    CustomerName VARCHAR(50),
    CustomerCity VARCHAR(50),
    ProductCode VARCHAR(10)
);

CREATE TABLE StoreOrders (
    OrderID INT,
    CustomerName VARCHAR(50),
    CustomerCity VARCHAR(50),
    ProductCode VARCHAR(10)
);

INSERT INTO OnlineOrders (OrderID, CustomerName, CustomerCity, ProductCode)
VALUES
(101, 'Aarav Mehta', 'Delhi', 'P100'),
(102, 'Meera Nair', 'Mumbai', 'P200'),
(103, 'Aarav Mehta', 'Delhi', 'P100'),
(104, 'Kavya Singh', 'Pune', 'P300'),
(105, 'Riya Das', 'Chennai', 'P400');

INSERT INTO StoreOrders (OrderID, CustomerName, CustomerCity, ProductCode)
VALUES
(201, 'Meera Nair', 'Mumbai', 'P200'),
(202, 'Mohit Verma', 'Delhi', 'P500'),
(203, 'Aarav Mehta', 'Delhi', 'P100'),
(204, 'Sana Khan', 'Hyderabad', 'P600'),
(205, 'Riya Das', 'Chennai', 'P400'),
(206, 'Sana Khan', 'Hyderabad', 'P600');
```

Use these tables throughout:

* `OnlineOrders(OrderID, CustomerName, CustomerCity, ProductCode)`
* `StoreOrders(OrderID, CustomerName, CustomerCity, ProductCode)`

#### 1. A sales report needs one unique list of customer cities. The list comes from `OnlineOrders` and `StoreOrders`.

Which set operator should you use? Explain why.

<details>

<summary>Solution</summary>

Use `UNION`.

It combines both result sets and returns each city once.

</details>

#### 2. The tables `OnlineOrders(OrderID, CustomerCity)` and `StoreOrders(OrderID, CustomerCity)` contain order data.

Write a query to show one unique list of customer cities from both tables.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCity
FROM OnlineOrders
UNION
SELECT CustomerCity
FROM StoreOrders;
```

`UNION` removes repeated city names.

</details>

#### 3. What happens when `UNION` finds the same row in both query results?

* A. It returns the row twice.
* B. It returns the row once.
* C. It returns `NULL`.
* D. It returns an error.

<details>

<summary>Solution</summary>

**B. It returns the row once.**

`UNION` removes duplicate rows from the final result.

</details>

#### 4. Write a query to produce one unique customer list from both sales channels.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerName
FROM OnlineOrders
UNION
SELECT CustomerName
FROM StoreOrders;
```

Both queries return one compatible column. Duplicate names are removed.

</details>

#### 5.Write one query to return unique customer-and-city pairs from both sales channels.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerName, CustomerCity
FROM OnlineOrders
UNION
SELECT CustomerName, CustomerCity
FROM StoreOrders;
```

A duplicate exists only when both selected values match.

</details>

#### 6. `UNION` requires both queries to return the same number of columns.(True/False)

<details>

<summary>Solution</summary>

**True.**

Both queries need the same number of selected columns.

</details>

#### 7. Write a query to show unique product codes from both sales channels.

<details>

<summary>Solution</summary>

```sql
SELECT ProductCode
FROM OnlineOrders
UNION
SELECT ProductCode
FROM StoreOrders;
```

</details>

#### 8. Write a query to show unique customer-and-product pairs from both sales channels.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerName, ProductCode
FROM OnlineOrders
UNION
SELECT CustomerName, ProductCode
FROM StoreOrders;
```

</details>

#### 9. Write a query to show every product code from both sales channels. Keep repeated values.

<details>

<summary>Solution</summary>

```sql
SELECT ProductCode
FROM OnlineOrders
UNION ALL
SELECT ProductCode
FROM StoreOrders;
```

`UNION ALL` retains every returned row.

</details>

#### 10. Complete the query so that duplicate product codes remain in the result.

```sql
SELECT ProductCode FROM OnlineOrders
_________
SELECT ProductCode FROM StoreOrders;
```

<details>

<summary>Solution</summary>

```sql
SELECT ProductCode FROM OnlineOrders
UNION ALL
SELECT ProductCode FROM StoreOrders;
```

</details>

#### 11. Write a query that returns all customer-and-city rows from both sales channels. Keep matching rows.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerName, CustomerCity
FROM OnlineOrders
UNION ALL
SELECT CustomerName, CustomerCity
FROM StoreOrders;
```

Matching rows remain because `UNION ALL` does not remove duplicates.

</details>

#### 12. Write a query to return every customer city from both sales channels. A repeated city must remain repeated.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCity
FROM OnlineOrders
UNION ALL
SELECT CustomerCity
FROM StoreOrders;
```

This keeps all rows from both tables.

</details>

#### 13. Which operator keeps every duplicate row?

* A. `UNION`
* B. `UNION ALL`
* C. `INTERSECT`
* D. `EXCEPT`

<details>

<summary>Solution</summary>

**B. `UNION ALL`**

</details>

#### 14. Write a query to show every customer name from both sales channels. Keep duplicates.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerName
FROM OnlineOrders
UNION ALL
SELECT CustomerName
FROM StoreOrders;
```

</details>

#### 15.Write a query to show every customer-and-product pair from both sales channels. Keep repeated pairs.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerName, ProductCode
FROM OnlineOrders
UNION ALL
SELECT CustomerName, ProductCode
FROM StoreOrders;
```

</details>

#### 16. A retailer wants products listed in both its online and store catalogues. Which set operator returns only those common products?

<details>

<summary>Solution</summary>

Use `INTERSECT`.

It returns rows present in both query results.

</details>

#### 17. Write a query to show product codes sold through both sales channels.

<details>

<summary>Solution</summary>

```sql
SELECT ProductCode
FROM OnlineOrders
INTERSECT
SELECT ProductCode
FROM StoreOrders;
```

</details>

#### 18. `INTERSECT` returns rows that appear in the first query only.(True/False)

<details>

<summary>Solution</summary>

**False.**

`INTERSECT` returns rows common to both queries.

</details>

#### 19. Write a query to identify customers who placed orders through both sales channels.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerName
FROM OnlineOrders
INTERSECT
SELECT CustomerName
FROM StoreOrders;
```

</details>

#### 20.Write a query to return customer-and-city pairs that occur in both sales channels.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerName, CustomerCity
FROM OnlineOrders
INTERSECT
SELECT CustomerName, CustomerCity
FROM StoreOrders;
```

Both values must match for a row to be common.

</details>

#### 21. Complete the query to return product codes found in both tables.

```sql
SELECT ProductCode FROM OnlineOrders
_________
SELECT ProductCode FROM StoreOrders;
```

<details>

<summary>Solution</summary>

```sql
SELECT ProductCode FROM OnlineOrders
INTERSECT
SELECT ProductCode FROM StoreOrders;
```

</details>

#### 22.Write a query to show cities that appear in both sales channels.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCity
FROM OnlineOrders
INTERSECT
SELECT CustomerCity
FROM StoreOrders;
```

</details>

#### 23. Write a query to show product codes sold online but not in stores.

<details>

<summary>Solution</summary>

```sql
SELECT ProductCode
FROM OnlineOrders
EXCEPT
SELECT ProductCode
FROM StoreOrders;
```

</details>

#### 24. Which query returns rows from `TableA` that do not appear in `TableB`?

* A. `SELECT Code FROM TableA UNION SELECT Code FROM TableB;`
* B. `SELECT Code FROM TableA UNION ALL SELECT Code FROM TableB;`
* C. `SELECT Code FROM TableA INTERSECT SELECT Code FROM TableB;`
* D. `SELECT Code FROM TableA EXCEPT SELECT Code FROM TableB;`

<details>

<summary>Solution</summary>

**D.**

`EXCEPT` subtracts the second result set from the first.

</details>

#### 25. Write a query to show customers who bought online but did not buy in stores.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerName
FROM OnlineOrders
EXCEPT
SELECT CustomerName
FROM StoreOrders;
```

</details>

#### 26. Write a query to show customer-and-city pairs that appeared online but not in stores.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerName, CustomerCity
FROM OnlineOrders
EXCEPT
SELECT CustomerName, CustomerCity
FROM StoreOrders;
```

</details>

#### 27. Write a query to show cities that appear online but do not appear in stores.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCity
FROM OnlineOrders
EXCEPT
SELECT CustomerCity
FROM StoreOrders;
```

</details>
