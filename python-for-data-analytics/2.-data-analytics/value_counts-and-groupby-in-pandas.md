# value\_counts and groupby in pandas

When we are dealing with dataset, we need to often summarize and find hidden insights from the data. `value_counts()` and `groupby()` functions are used to summarize and find meaningful information from the dataset.

We are going to work on adidas data and find meaningful information using `value_counts()` and `groupby()` functions.

## value\_counts()

`value_counts()` function is used to count the unique values in columns.

Example — load data and create a total column:

{% code title="load_data.py" %}
```python
import pandas as pd

df = pd.read_excel('Adidas US Sales Datasets.xlsx')
df['total'] = df['Price per Unit'] * df['Units Sold']
df.head(90)
```
{% endcode %}

Out\[56]:

|     | Retailer      | Invoice Date | Region    | State    | City     | Product                   | Price per Unit | Units Sold | Sales Method |   total |
| --: | ------------- | ------------ | --------- | -------- | -------- | ------------------------- | -------------- | ---------: | ------------ | ------: |
|   0 | Foot Locker   | 2020-01-01   | Northeast | New York | New York | Men's Street Footwear     | 50.0           |       1200 | In-store     | 60000.0 |
|   1 | Foot Locker   | 2020-01-02   | Northeast | New York | New York | Men's Athletic Footwear   | 50.0           |       1000 | In-store     | 50000.0 |
|   2 | Foot Locker   | 2020-01-03   | Northeast | New York | New York | Women's Street Footwear   | 40.0           |       1000 | In-store     | 40000.0 |
|   3 | Foot Locker   | 2020-01-04   | Northeast | New York | New York | Women's Athletic Footwear | 45.0           |        850 | In-store     | 38250.0 |
|   4 | Foot Locker   | 2020-01-05   | Northeast | New York | New York | Men's Apparel             | 60.0           |        900 | In-store     | 54000.0 |
| ... | ...           | ...          | ...       | ...      | ...      | ...                       | ...            |        ... | ...          |     ... |
|  85 | Sports Direct | 2020-08-05   | South     | Texas    | Houston  | Women's Apparel           | 40.0           |        650 | Outlet       | 26000.0 |
|  86 | Sports Direct | 2020-08-06   | South     | Texas    | Houston  | Men's Street Footwear     | 30.0           |        900 | Outlet       | 27000.0 |
|  87 | Sports Direct | 2020-08-07   | South     | Texas    | Houston  | Men's Athletic Footwear   | 40.0           |        900 | Outlet       | 36000.0 |
|  88 | Sports Direct | 2020-08-08   | South     | Texas    | Houston  | Women's Street Footwear   | 35.0           |        725 | Outlet       | 25375.0 |
|  89 | Sports Direct | 2020-08-09   | South     | Texas    | Houston  | Women's Athletic Footwear | 40.0           |        625 | Outlet       | 25000.0 |

90 rows × 10 columns

### value\_counts() the Retailer

Counts all unique values of `Retailer`. Results in descending order.

In \[37]:

```python
df['Retailer'].value_counts()
```

Out\[37]:

Retailer\
Foot Locker 2637\
West Gear 2374\
Sports Direct 2032\
Kohl's 1030\
Amazon 949\
Walmart 626\
Name: count, dtype: int64

Insight: Foot Locker is one of the biggest players for Adidas sales.

### value\_counts(normalize=True) for Retailer

Shows proportions.

In \[38]:

```python
df['Retailer'].value_counts(normalize=True)
```

Out\[38]:

Retailer\
Foot Locker 0.273321\
West Gear 0.246061\
Sports Direct 0.210614\
Kohl's 0.106758\
Amazon 0.098362\
Walmart 0.064884\
Name: proportion, dtype: float64

Note: Sum is 1.

### value\_counts(normalize=True) \* 100 for Retailer

Shows percentages.

In \[39]:

```python
df['Retailer'].value_counts(normalize=True) * 100
```

Out\[39]:

Retailer\
Foot Locker 27.332090\
West Gear 24.606136\
Sports Direct 21.061360\
Kohl's 10.675788\
Amazon 9.836235\
Walmart 6.488391\
Name: proportion, dtype: float64

### Value Counts for Region

In \[40]:

```python
df['Region'].value_counts()
```

Out\[40]:

Region\
West 2448\
Northeast 2376\
Midwest 1872\
South 1728\
Southeast 1224\
Name: count, dtype: int64

In \[41]:

```python
df['Region'].value_counts(normalize=True)
```

Out\[41]:

Region\
West 0.253731\
Northeast 0.246269\
Midwest 0.194030\
South 0.179104\
Southeast 0.126866\
Name: proportion, dtype: float64

In \[42]:

```python
df['Region'].value_counts(normalize=True) * 100
```

Out\[42]:

Region\
West 25.373134\
Northeast 24.626866\
Midwest 19.402985\
South 17.910448\
Southeast 12.686567\
Name: proportion, dtype: float64

`value_counts()` always gives result in descending order. To keep original order, use `sort=False`.

In \[43]:

```python
df['Region'].value_counts(sort=False)
```

Out\[43]:

Region\
Northeast 2376\
South 1728\
West 2448\
Midwest 1872\
Southeast 1224\
Name: count, dtype: int64

## Multiple Columns in value\_counts()

Count combinations of columns:

In \[44]:

```python
df[['Region','Retailer']].value_counts()
```

Out\[44]:

Region Retailer\
West West Gear 1207\
Midwest Foot Locker 840\
Northeast Foot Locker 835\
South Sports Direct 732\
West Kohl's 550\
Northeast Amazon 541\
Sports Direct 462\
Southeast Sports Direct 427\
Foot Locker 422\
South West Gear 408\
West Foot Locker 396\
Midwest West Gear 366\
South Walmart 366\
... (truncated) Name: count, dtype: int64

Use `sort=False` to keep the order as in the data:

In \[45]:

```python
df[['Region','Retailer']].value_counts(sort=False)
```

Out\[45]:

Region Retailer\
Midwest Amazon 136\
Foot Locker 840\
Kohl's 244\
Sports Direct 286\
West Gear 366\
Northeast Amazon 541\
... (truncated) Name: count, dtype: int64

Note: `value_counts()` converts the counted columns into an index. Use `reset_index()` to get them back as columns.

In \[46]:

```python
mdf = df[['Region','Retailer']].value_counts(sort=False).reset_index()
mdf
```

Out\[46]:

|    | Region    | Retailer      | count |
| -: | --------- | ------------- | ----: |
|  0 | Midwest   | Amazon        |   136 |
|  1 | Midwest   | Foot Locker   |   840 |
|  2 | Midwest   | Kohl's        |   244 |
|  3 | Midwest   | Sports Direct |   286 |
|  4 | Midwest   | West Gear     |   366 |
|  5 | Northeast | Amazon        |   541 |
|  6 | Northeast | Foot Locker   |   835 |
|  7 | Northeast | Kohl's        |   170 |
|  8 | Northeast | Sports Direct |   462 |
|  9 | Northeast | Walmart       |    66 |
| 10 | Northeast | West Gear     |   302 |
| 11 | South     | Amazon        |    12 |
| 12 | South     | Foot Locker   |   144 |
| 13 | South     | Kohl's        |    66 |
| 14 | South     | Sports Direct |   732 |
| 15 | South     | Walmart       |   366 |
| 16 | South     | West Gear     |   408 |
| 17 | Southeast | Amazon        |   134 |
| 18 | Southeast | Foot Locker   |   422 |
| 19 | Southeast | Sports Direct |   427 |
| 20 | Southeast | Walmart       |   150 |
| 21 | Southeast | West Gear     |    91 |
| 22 | West      | Amazon        |   126 |
| 23 | West      | Foot Locker   |   396 |
| 24 | West      | Kohl's        |   550 |
| 25 | West      | Sports Direct |   125 |
| 26 | West      | Walmart       |    44 |
| 27 | West      | West Gear     |  1207 |

You can sort to find top players in each region:

In \[47]:

```python
mdf = mdf.sort_values(['Region','count'], ascending=False)
mdf
```

Out\[47]: (sorted by Region then count, descending within each region)

|    | Region    | Retailer      | count |
| -: | --------- | ------------- | ----: |
| 27 | West      | West Gear     |  1207 |
| 24 | West      | Kohl's        |   550 |
| 23 | West      | Foot Locker   |   396 |
| 22 | West      | Amazon        |   126 |
| 25 | West      | Sports Direct |   125 |
| 26 | West      | Walmart       |    44 |
| 19 | Southeast | Sports Direct |   427 |
| 18 | Southeast | Foot Locker   |   422 |
| 20 | Southeast | Walmart       |   150 |
| 17 | Southeast | Amazon        |   134 |
| 21 | Southeast | West Gear     |    91 |
| 14 | South     | Sports Direct |   732 |
| 16 | South     | West Gear     |   408 |
| 15 | South     | Walmart       |   366 |
| 12 | South     | Foot Locker   |   144 |
| 13 | South     | Kohl's        |    66 |
| 11 | South     | Amazon        |    12 |
|  6 | Northeast | Foot Locker   |   835 |
|  5 | Northeast | Amazon        |   541 |
|  8 | Northeast | Sports Direct |   462 |
| 10 | Northeast | West Gear     |   302 |
|  7 | Northeast | Kohl's        |   170 |
|  9 | Northeast | Walmart       |    66 |
|  1 | Midwest   | Foot Locker   |   840 |
|  4 | Midwest   | West Gear     |   366 |
|  3 | Midwest   | Sports Direct |   286 |
|  2 | Midwest   | Kohl's        |   244 |
|  0 | Midwest   | Amazon        |   136 |

## Groupby in Pandas

`groupby` in pandas is used to group data and perform aggregate functions.

### groupby Region and Find Total Sales

In \[48]:

```python
mdf = df.groupby('Region').agg(total_sales=('total','sum'))
mdf
```

Out\[48]:

| Region    | total\_sales |
| --------- | ------------ |
| Midwest   | 16674434.0   |
| Northeast | 25078267.0   |
| South     | 20603356.0   |
| Southeast | 21374436.0   |
| West      | 36436157.0   |

### groupby Region and Retailer and Find Total Sales

In \[49]:

```python
mdf = df.groupby(['Region','Retailer']).agg(total_sales=('total','sum'))
mdf
```

Out\[49]:

| Region    | Retailer      | total\_sales |
| --------- | ------------- | ------------ |
| Midwest   | Amazon        | 2068448.0    |
| Midwest   | Foot Locker   | 5888769.0    |
| Midwest   | Kohl's        | 2731365.0    |
| Midwest   | Sports Direct | 3219616.0    |
| Midwest   | West Gear     | 2766236.0    |
| Northeast | Amazon        | 4998840.0    |
| Northeast | Foot Locker   | 8991649.0    |
| Northeast | Kohl's        | 1723218.0    |
| Northeast | Sports Direct | 3404772.0    |
| Northeast | Walmart       | 1968355.0    |
| Northeast | West Gear     | 3991433.0    |
| South     | Amazon        | 58091.0      |
| South     | Foot Locker   | 1322450.0    |
| South     | Kohl's        | 506680.0     |
| South     | Sports Direct | 9292971.0    |
| South     | Walmart       | 4712683.0    |
| South     | West Gear     | 4710481.0    |
| Southeast | Amazon        | 1332008.0    |
| Southeast | Foot Locker   | 7768368.0    |
| Southeast | Sports Direct | 7040593.0    |
| Southeast | Walmart       | 2992039.0    |
| Southeast | West Gear     | 2241428.0    |
| West      | Amazon        | 1639600.0    |
| West      | Foot Locker   | 5053709.0    |
| West      | Kohl's        | 8551190.0    |
| West      | Sports Direct | 1658670.0    |
| West      | Walmart       | 833008.0     |
| West      | West Gear     | 18699980.0   |

Note: `groupby()` converts grouped columns into index. Use `reset_index()` to bring them back as columns.

In \[51]:

```python
mdf = df.groupby(['Region','Retailer']).agg(total_sales=('total','sum')).reset_index()
mdf
```

Out\[51]:

|    | Region    | Retailer      | total\_sales |
| -: | --------- | ------------- | ------------ |
|  0 | Midwest   | Amazon        | 2068448.0    |
|  1 | Midwest   | Foot Locker   | 5888769.0    |
|  2 | Midwest   | Kohl's        | 2731365.0    |
|  3 | Midwest   | Sports Direct | 3219616.0    |
|  4 | Midwest   | West Gear     | 2766236.0    |
|  5 | Northeast | Amazon        | 4998840.0    |
|  6 | Northeast | Foot Locker   | 8991649.0    |
|  7 | Northeast | Kohl's        | 1723218.0    |
|  8 | Northeast | Sports Direct | 3404772.0    |
|  9 | Northeast | Walmart       | 1968355.0    |
| 10 | Northeast | West Gear     | 3991433.0    |
| 11 | South     | Amazon        | 58091.0      |
| 12 | South     | Foot Locker   | 1322450.0    |
| 13 | South     | Kohl's        | 506680.0     |
| 14 | South     | Sports Direct | 9292971.0    |
| 15 | South     | Walmart       | 4712683.0    |
| 16 | South     | West Gear     | 4710481.0    |
| 17 | Southeast | Amazon        | 1332008.0    |
| 18 | Southeast | Foot Locker   | 7768368.0    |
| 19 | Southeast | Sports Direct | 7040593.0    |
| 20 | Southeast | Walmart       | 2992039.0    |
| 21 | Southeast | West Gear     | 2241428.0    |
| 22 | West      | Amazon        | 1639600.0    |
| 23 | West      | Foot Locker   | 5053709.0    |
| 24 | West      | Kohl's        | 8551190.0    |
| 25 | West      | Sports Direct | 1658670.0    |
| 26 | West      | Walmart       | 833008.0     |
| 27 | West      | West Gear     | 18699980.0   |

You can sort these results as needed.

In \[52]:

```python
mdf = mdf.sort_values(['Region','Retailer'], ascending=False)
mdf
```

Out\[52]: (sorted view)

|    | Region    | Retailer      | total\_sales |
| -: | --------- | ------------- | ------------ |
| 27 | West      | West Gear     | 18699980.0   |
| 26 | West      | Walmart       | 833008.0     |
| 25 | West      | Sports Direct | 1658670.0    |
| 24 | West      | Kohl's        | 8551190.0    |
| 23 | West      | Foot Locker   | 5053709.0    |
| 22 | West      | Amazon        | 1639600.0    |
| 21 | Southeast | West Gear     | 2241428.0    |
| 20 | Southeast | Walmart       | 2992039.0    |
| 19 | Southeast | Sports Direct | 7040593.0    |
| 18 | Southeast | Foot Locker   | 7768368.0    |
| 17 | Southeast | Amazon        | 1332008.0    |
| 16 | South     | West Gear     | 4710481.0    |
| 15 | South     | Walmart       | 4712683.0    |
| 14 | South     | Sports Direct | 9292971.0    |
| 13 | South     | Kohl's        | 506680.0     |
| 12 | South     | Foot Locker   | 1322450.0    |
| 11 | South     | Amazon        | 58091.0      |
| 10 | Northeast | West Gear     | 3991433.0    |
|  9 | Northeast | Walmart       | 1968355.0    |
|  8 | Northeast | Sports Direct | 3404772.0    |
|  7 | Northeast | Kohl's        | 1723218.0    |
|  6 | Northeast | Foot Locker   | 8991649.0    |
|  5 | Northeast | Amazon        | 4998840.0    |
|  4 | Midwest   | West Gear     | 2766236.0    |
|  3 | Midwest   | Sports Direct | 3219616.0    |
|  2 | Midwest   | Kohl's        | 2731365.0    |
|  1 | Midwest   | Foot Locker   | 5888769.0    |
|  0 | Midwest   | Amazon        | 2068448.0    |

### groupby the region and find total sales, number of sales, avg sales, max sales

In \[53]:

```python
mdf = df.groupby('Region').agg(
    total_sales=('total','sum'),
    number_of_sales=('Region','count'),
    avg_sales=('total','mean'),
    max_sales=('total','max'),
)
mdf
```

Out\[53]:

| Region    | total\_sales | number\_of\_sales |   avg\_sales | max\_sales |
| --------- | ------------ | ----------------: | -----------: | ---------: |
| Midwest   | 16674434.0   |              1872 |  8907.283120 |    61875.0 |
| Northeast | 25078267.0   |              2376 | 10554.826178 |    78000.0 |
| South     | 20603356.0   |              1728 | 11923.238426 |    82500.0 |
| Southeast | 21374436.0   |              1224 | 17462.774510 |    82500.0 |
| West      | 36436157.0   |              2448 | 14884.051062 |    73500.0 |

### groupby the region and retailer and find total sales, number of sales, avg sales, max sales

In \[54]:

```python
mdf = df.groupby(['Region','Retailer']).agg(
    total_sales=('total','sum'),
    number_of_sales=('Region','count'),
    avg_sales=('total','mean'),
    max_sales=('total','max'),
)
mdf
```

Out\[54]: (grouped by Region & Retailer with aggregations)

| Region    | Retailer      | total\_sales | number\_of\_sales |   avg\_sales | max\_sales |
| --------- | ------------- | ------------ | ----------------: | -----------: | ---------: |
| Midwest   | Amazon        | 2068448.0    |               136 | 15209.176471 |    61875.0 |
| Midwest   | Foot Locker   | 5888769.0    |               840 |  7010.439286 |    42250.0 |
| Midwest   | Kohl's        | 2731365.0    |               244 | 11194.118852 |    39000.0 |
| Midwest   | Sports Direct | 3219616.0    |               286 | 11257.398601 |    54000.0 |
| Midwest   | West Gear     | 2766236.0    |               366 |  7558.021858 |    50000.0 |
| Northeast | Amazon        | 4998840.0    |               541 |  9240.000000 |    45500.0 |
| Northeast | Foot Locker   | 8991649.0    |               835 | 10768.441916 |    76500.0 |
| Northeast | Kohl's        | 1723218.0    |               170 | 10136.576471 |    47250.0 |
| Northeast | Sports Direct | 3404772.0    |               462 |  7369.636364 |    35750.0 |
| Northeast | Walmart       | 1968355.0    |                66 | 29823.560606 |    78000.0 |
| Northeast | West Gear     | 3991433.0    |               302 | 13216.665563 |    61750.0 |
| South     | Amazon        | 58091.0      |                12 |  4840.916667 |    18000.0 |
| South     | Foot Locker   | 1322450.0    |               144 |  9183.680556 |    56250.0 |
| South     | Kohl's        | 506680.0     |                66 |  7676.969697 |    43750.0 |
| South     | Sports Direct | 9292971.0    |               732 | 12695.315574 |    54250.0 |
| South     | Walmart       | 4712683.0    |               366 | 12876.183060 |    50000.0 |
| South     | West Gear     | 4710481.0    |               408 | 11545.296569 |    82500.0 |
| Southeast | Amazon        | 1332008.0    |               134 |  9940.358209 |    58125.0 |
| Southeast | Foot Locker   | 7768368.0    |               422 | 18408.454976 |    75250.0 |
| Southeast | Sports Direct | 7040593.0    |               427 | 16488.508197 |    69875.0 |
| Southeast | Walmart       | 2992039.0    |               150 | 19946.926667 |    82500.0 |
| Southeast | West Gear     | 2241428.0    |                91 | 24631.076923 |    74750.0 |
| West      | Amazon        | 1639600.0    |               126 | 13012.698413 |    45000.0 |
| West      | Foot Locker   | 5053709.0    |               396 | 12761.891414 |    65000.0 |
| West      | Kohl's        | 8551190.0    |               550 | 15547.618182 |    52000.0 |
| West      | Sports Direct | 1658670.0    |               125 | 13269.360000 |    49875.0 |
| West      | Walmart       | 833008.0     |                44 | 18932.000000 |    59500.0 |
| West      | West Gear     | 18699980.0   |              1207 | 15492.941176 |    73500.0 |

## Assignments

<details>

<summary>VALUE_COUNTS — 25 Questions (Fully Cleaned, Logical)</summary>

* Which retailer has the most transactions?
* Which region has the highest number of transactions?
* How many transactions are recorded per state?
* Which city appears most frequently?
* What’s the distribution of store types (In-store, Outlet)?
* Which product category appears most often?
* How many transactions belong to Men’s vs Women’s categories?
* Which retailer–region combination occurs most frequently?
* Which retailer–store type combination appears most often?
* Which region–store type pairing occurs most frequently?
* Which category dominates in each region?
* How often does each rounded price point (nearest 10) occur?
* Which retailer offers the most variety of categories?
* Which region records the most apparel transactions?
* Which retailer focuses more on footwear products?
* Which city contributes the most to women’s products?
* Which category dominates in Houston?
* Which region has more athletic footwear transactions?
* Which retailer operates in the most regions?
* What’s the most frequent category–store type combination?
* Which retailer sells the widest range of store types?
* Which region contributes the most to men’s apparel?
* Which category–region pair appears most frequently?
* Count of state–category combinations that appear more than twice.
* Which store type dominates overall across all regions?

</details>

<details>

<summary>GROUPBY — 25 Questions (Fully Cleaned, Logical)</summary>

* Total sales per retailer.
* Total sales per region.
* Average price per product category.
* Total units sold per region.
* Average sales per transaction by store type.
* Total sales per state, sorted from highest to lowest.
* Average price by gender segment (Men’s vs Women’s).
* Total sales by region and retailer.
* Average units sold per retailer.
* Total revenue per category in New York.
* Compare total sales for In-store vs Outlet per region.
* Which product category generated the highest total sales?
* Which region has the highest average revenue per transaction?
* Total sales by retailer and product category.
* Average price per region and store type.
* For each city, find the category with maximum total sales.
* Average units sold for each retailer–category pair.
* Total sales and average price per retailer (agg usage).
* Total sales for men’s vs women’s per retailer.
* Highest average price category per region.
* Compare total units sold for Street vs Athletic Footwear.
* Find percentage contribution of each retailer to total sales.
* For each retailer, find the best-performing store type by sales.
* Total sales per region–category pair.
* Calculate average units sold per transaction for each store type.

</details>
