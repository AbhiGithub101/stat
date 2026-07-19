# Group By, Aggregate Functions & Having Clause

### Sample data

Use this table for all questions on this page.

#### Create the table

```sql
CREATE TABLE SalesOrders (
    OrderID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    CustomerCity VARCHAR(50),
    ProductCategory VARCHAR(50),
    Salesperson VARCHAR(100),
    OrderAmount DECIMAL(10,2),
    Quantity INT,
    OrderDate DATE,
    OrderStatus VARCHAR(20)
);
```

#### Insert sample data

```sql
INSERT INTO SalesOrders (OrderID, CustomerName, CustomerCity, ProductCategory, Salesperson, OrderAmount, Quantity, OrderDate, OrderStatus)
VALUES
(1001, 'Aditi Shah', 'Mumbai', 'Electronics', 'Rohan Mehta', 2500.00, 1, '2024-01-05', 'Completed'),
(1002, 'Aman Verma', 'Delhi', 'Stationery', 'Priya Nair', 800.00, 10, '2024-01-07', 'Completed'),
(1003, 'Neha Kapoor', 'Mumbai', 'Furniture', 'Rohan Mehta', 5400.00, 2, '2024-01-10', 'Pending'),
(1004, 'Vikram Jain', 'Pune', 'Electronics', 'Anita Rao', 3200.00, 1, '2024-01-12', 'Completed'),
(1005, 'Sara Ali', 'Delhi', 'Furniture', 'Priya Nair', 2100.00, 1, '2024-01-15', 'Completed'),
(1006, 'Karan Patel', 'Ahmedabad', 'Stationery', 'Anita Rao', 600.00, 12, '2024-01-17', 'Cancelled'),
(1007, 'Meera Iyer', 'Chennai', 'Electronics', 'Rohan Mehta', 4700.00, 2, '2024-01-20', 'Completed'),
(1008, 'Rahul Das', 'Kolkata', 'Accessories', 'Priya Nair', 1500.00, 3, '2024-01-22', 'Completed'),
(1009, 'Pooja Singh', 'Pune', 'Furniture', 'Anita Rao', 2800.00, 1, '2024-01-25', 'Pending'),
(1010, 'Arjun Nair', 'Mumbai', 'Accessories', 'Rohan Mehta', 900.00, 4, '2024-01-28', 'Completed'),
(1011, 'Divya Sharma', 'Delhi', 'Electronics', 'Priya Nair', 3900.00, 1, '2024-02-01', 'Completed'),
(1012, 'Nitin Gupta', 'Ahmedabad', 'Furniture', 'Anita Rao', 2600.00, 1, '2024-02-03', 'Completed');
```

#### Check the data

```sql
SELECT *
FROM SalesOrders;
```

Use this structure in all questions:

* `SalesOrders(OrderID, CustomerName, CustomerCity, ProductCategory, Salesperson, OrderAmount, Quantity, OrderDate, OrderStatus)`

### Aggregate functions questions

#### 1. What does `COUNT(*)` do in SQL Server?

<details>

<summary>Solution</summary>

`COUNT(*)` returns the total number of rows.

It counts every row in the result.

</details>

2\. Write a query to find the total number of orders.

<details>

<summary>Solution</summary>

```sql
SELECT COUNT(*) AS TotalOrders
FROM SalesOrders;
```

</details>

#### 3. Write a query to find the total order amount of all orders.

<details>

<summary>Solution</summary>

```sql
SELECT SUM(OrderAmount) AS TotalOrderAmount
FROM SalesOrders;
```

</details>

#### 4. Write a query to find the average order amount.

<details>

<summary>Solution</summary>

```sql
SELECT AVG(OrderAmount) AS AverageOrderAmount
FROM SalesOrders;
```

</details>

#### 5. Write a query to find the highest order amount.

<details>

<summary>Solution</summary>

```sql
SELECT MAX(OrderAmount) AS HighestOrderAmount
FROM SalesOrders;
```

</details>

#### 6. Write a query to find the lowest order amount.

<details>

<summary>Solution</summary>

```sql
SELECT MIN(OrderAmount) AS LowestOrderAmount
FROM SalesOrders;
```

</details>

#### 7. Write a query to find the total quantity sold.

<details>

<summary>Solution</summary>

```sql
SELECT SUM(Quantity) AS TotalQuantitySold
FROM SalesOrders;
```

</details>

#### 8. Write a query to find the total completed sales amount.

<details>

<summary>Solution</summary>

```sql
SELECT SUM(OrderAmount) AS TotalCompletedSales
FROM SalesOrders
WHERE OrderStatus = 'Completed';
```

</details>

### GROUP BY questions

#### 1. Write a query to show each city and the number of orders from that city.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCity, COUNT(*) AS TotalOrders
FROM SalesOrders
GROUP BY CustomerCity;
```

</details>

#### 2. Write a query to show each salesperson and the number of orders handled by them.

<details>

<summary>Solution</summary>

```sql
SELECT Salesperson, COUNT(*) AS TotalOrders
FROM SalesOrders
GROUP BY Salesperson;
```

</details>

#### 3. Write a query to show each product category and the total quantity sold.

<details>

<summary>Solution</summary>

```sql
SELECT ProductCategory, SUM(Quantity) AS TotalQuantity
FROM SalesOrders
GROUP BY ProductCategory;
```

</details>

#### 4. Write a query to show each order status and the total number of orders.

<details>

<summary>Solution</summary>

```sql
SELECT OrderStatus, COUNT(*) AS TotalOrders
FROM SalesOrders
GROUP BY OrderStatus;
```

</details>

#### 5. Write a query to show each product category and the average order amount.

<details>

<summary>Solution</summary>

```sql
SELECT ProductCategory, AVG(OrderAmount) AS AverageOrderAmount
FROM SalesOrders
GROUP BY ProductCategory;
```

</details>

#### 6. Write a query to show each city and the total sales amount. Sort the result from highest to lowest total sales.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCity, SUM(OrderAmount) AS TotalSales
FROM SalesOrders
GROUP BY CustomerCity
ORDER BY TotalSales DESC;
```

</details>

#### 7. Write a query to show each salesperson and the highest order amount handled by them.

<details>

<summary>Solution</summary>

```sql
SELECT Salesperson, MAX(OrderAmount) AS HighestOrderAmount
FROM SalesOrders
GROUP BY Salesperson;
```

</details>

#### 8. Write a query to show each salesperson and each order status with the number of orders in each combination.

<details>

<summary>Solution</summary>

```sql
SELECT Salesperson, OrderStatus, COUNT(*) AS TotalOrders
FROM SalesOrders
GROUP BY Salesperson, OrderStatus;
```

</details>

### HAVING clause questions

#### 1. Write a query to show salespersons who handled more than 3 orders.

<details>

<summary>Solution</summary>

```sql
SELECT Salesperson, COUNT(*) AS TotalOrders
FROM SalesOrders
GROUP BY Salesperson
HAVING COUNT(*) > 3;
```

</details>

#### 2. Write a query to show cities where the total sales amount is greater than `5000`.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCity, SUM(OrderAmount) AS TotalSales
FROM SalesOrders
GROUP BY CustomerCity
HAVING SUM(OrderAmount) > 5000;
```

</details>

#### 3. Write a query to show product categories where the average order amount is greater than `3000`.

<details>

<summary>Solution</summary>

```sql
SELECT ProductCategory, AVG(OrderAmount) AS AverageOrderAmount
FROM SalesOrders
GROUP BY ProductCategory
HAVING AVG(OrderAmount) > 3000;
```

</details>

#### 4. Write a query to show order statuses that have at least 2 orders.

<details>

<summary>Solution</summary>

```sql
SELECT OrderStatus, COUNT(*) AS TotalOrders
FROM SalesOrders
GROUP BY OrderStatus
HAVING COUNT(*) >= 2;
```

</details>

#### 5. Write a query to show salespersons whose maximum order amount is greater than `4000`.

<details>

<summary>Solution</summary>

```sql
SELECT Salesperson, MAX(OrderAmount) AS HighestOrderAmount
FROM SalesOrders
GROUP BY Salesperson
HAVING MAX(OrderAmount) > 4000;
```

</details>

#### 6. Write a query to show salespersons whose total completed sales amount is greater than `5000`.

<details>

<summary>Solution</summary>

```sql
SELECT Salesperson, SUM(OrderAmount) AS TotalCompletedSales
FROM SalesOrders
WHERE OrderStatus = 'Completed'
GROUP BY Salesperson
HAVING SUM(OrderAmount) > 5000;
```

</details>

#### 7. Write a query to show cities that have more than 1 completed order.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCity, COUNT(*) AS TotalCompletedOrders
FROM SalesOrders
WHERE OrderStatus = 'Completed'
GROUP BY CustomerCity
HAVING COUNT(*) > 1;
```

</details>

### Challenging questions

#### 1. Write a query to show each salesperson and their total completed sales amount. Show only those salespersons whose total completed sales are more than `5000`. Sort the result from highest to lowest total sales.

<details>

<summary>Solution</summary>

```sql
SELECT Salesperson, SUM(OrderAmount) AS TotalCompletedSales
FROM SalesOrders
WHERE OrderStatus = 'Completed'
GROUP BY Salesperson
HAVING SUM(OrderAmount) > 5000
ORDER BY TotalCompletedSales DESC;
```

</details>

#### 2. Write a query to show each product category and the average order amount for only completed orders. Show only categories where the average amount is greater than `2000`.

<details>

<summary>Solution</summary>

```sql
SELECT ProductCategory, AVG(OrderAmount) AS AverageOrderAmount
FROM SalesOrders
WHERE OrderStatus = 'Completed'
GROUP BY ProductCategory
HAVING AVG(OrderAmount) > 2000;
```

</details>

#### 3. Write a query to show each city and the total number of completed orders. Show only cities with at least `2` completed orders.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCity, COUNT(*) AS TotalCompletedOrders
FROM SalesOrders
WHERE OrderStatus = 'Completed'
GROUP BY CustomerCity
HAVING COUNT(*) >= 2;
```

</details>

#### 4. Write a query to show each salesperson and the highest order amount handled by them in the `Electronics` category. Show only those salespersons whose highest amount is more than `3000`.

<details>

<summary>Solution</summary>

```sql
SELECT Salesperson, MAX(OrderAmount) AS HighestElectronicsOrder
FROM SalesOrders
WHERE ProductCategory = 'Electronics'
GROUP BY Salesperson
HAVING MAX(OrderAmount) > 3000;
```

</details>

#### 5. Write a query to show each city and the total quantity sold. Show only cities where total quantity is more than `3`. Sort the result by total quantity from high to low.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCity, SUM(Quantity) AS TotalQuantitySold
FROM SalesOrders
GROUP BY CustomerCity
HAVING SUM(Quantity) > 3
ORDER BY TotalQuantitySold DESC;
```

</details>

#### 6. Write a query to show each salesperson and order status with the total number of orders in each combination. Show only combinations where the count is greater than `1`.

<details>

<summary>Solution</summary>

```sql
SELECT Salesperson, OrderStatus, COUNT(*) AS TotalOrders
FROM SalesOrders
GROUP BY Salesperson, OrderStatus
HAVING COUNT(*) > 1;
```

</details>

#### 7. Write a query to show each product category and the total sales amount between `2024-01-01` and `2024-01-31`. Show only categories with total sales more than `4000`.

<details>

<summary>Solution</summary>

```sql
SELECT ProductCategory, SUM(OrderAmount) AS TotalSales
FROM SalesOrders
WHERE OrderDate BETWEEN '2024-01-01' AND '2024-01-31'
GROUP BY ProductCategory
HAVING SUM(OrderAmount) > 4000;
```

</details>

#### 8. Write a query to show each city and the average order amount, but only for orders that are not cancelled. Show only cities where the average amount is greater than `2500`.

<details>

<summary>Solution</summary>

```sql
SELECT CustomerCity, AVG(OrderAmount) AS AverageOrderAmount
FROM SalesOrders
WHERE OrderStatus <> 'Cancelled'
GROUP BY CustomerCity
HAVING AVG(OrderAmount) > 2500;
```

</details>
