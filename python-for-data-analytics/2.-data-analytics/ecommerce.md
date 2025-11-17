# ecommerce

Suppose you are working with an E-Commerce platform and you need to analyze and come up with many metrics and insights.

```python
import numpy as np
import pandas as pd
```

```python
df = pd.read_csv('new_retail_data.csv')
df
```

Out\[4]:

|        | Customer\_ID | Name                | City       | State           | Country   | Age  | Gender | Income | Customer\_Segment | Year   | Month     | Total\_Purchases | Amount     | Product\_Category | Product\_Brand | Product\_Type | Feedback  | Payment\_Method | Ratings | products           |
| ------ | ------------ | ------------------- | ---------- | --------------- | --------- | ---- | ------ | ------ | ----------------- | ------ | --------- | ---------------- | ---------- | ----------------- | -------------- | ------------- | --------- | --------------- | ------- | ------------------ |
| 0      | 37249.0      | Michelle Harrington | Dortmund   | Berlin          | Germany   | 21.0 | Male   | Low    | Regular           | 2023.0 | September | 3.0              | 108.028757 | Clothing          | Nike           | Shorts        | Excellent | Debit Card      | 5.0     | Cycling shorts     |
| 1      | 69749.0      | Kelsey Hill         | Nottingham | England         | UK        | 19.0 | Female | Low    | Premium           | 2023.0 | December  | 2.0              | 403.353907 | Electronics       | Samsung        | Tablet        | Excellent | Credit Card     | 4.0     | Lenovo Tab         |
| 2      | 30192.0      | Scott Jensen        | Geelong    | New South Wales | Australia | 48.0 | Male   | Low    | Regular           | 2023.0 | April     | 3.0              | 354.477600 | Books             | Penguin Books  | Children's    | Average   | Credit Card     | 2.0     | Sports equipment   |
| 3      | 62101.0      | Joseph Miller       | Edmonton   | Ontario         | Canada    | 56.0 | Male   | High   | Premium           | 2023.0 | May       | 7.0              | 352.407717 | Home Decor        | Home Depot     | Tools         | Excellent | PayPal          | 4.0     | Utility knife      |
| 4      | 27901.0      | Debra Coleman       | Bristol    | England         | UK        | 22.0 | Male   | Low    | Premium           | 2024.0 | January   | 2.0              | 124.276524 | Grocery           | Nestle         | Chocolate     | Bad       | Cash            | 1.0     | Chocolate cookies  |
| ...    | ...          | ...                 | ...        | ...             | ...       | ...  | ...    | ...    | ...               | ...    | ...       | ...              | ...        | ...               | ...            | ...           | ...       | ...             | ...     | ...                |
| 302005 | 12104.0      | Meagan Ellis        | Townsville | New South Wales | Australia | 31.0 | Male   | Medium | Regular           | 2024.0 | January   | 5.0              | 194.792597 | Books             | Penguin Books  | Fiction       | Bad       | Cash            | 1.0     | Historical fiction |
| 302006 | 69772.0      | Mathew Beck         | Hanover    | Berlin          | Germany   | 35.0 | Female | Low    | New               | 2023.0 | December  | 1.0              | 285.137301 | Electronics       | Apple          | Laptop        | Excellent | Cash            | 5.0     | LG Gram            |
| 302007 | 28449.0      | Daniel Lee          | Brighton   | England         | UK        | 41.0 | Male   | Low    | Premium           | 2024.0 | February  | 3.0              | 60.701761  | Clothing          | Adidas         | Jacket        | Average   | Cash            | 2.0     | Parka              |
| 302008 | 45477.0      | Patrick Wilson      | Halifax    | Ontario         | Canada    | 41.0 | Male   | Medium | New               | 2023.0 | September | 1.0              | 120.834784 | Home Decor        | IKEA           | Furniture     | Good      | Cash            | 4.0     | TV stand           |
| 302009 | 53626.0      | Dustin Merritt      | Tucson     | West Virginia   | USA       | 28.0 | Female | Low    | Premium           | 2024.0 | January   | 7.0              | 340.319059 | Home Decor        | Home Depot     | Decorations   | Average   | Cash            | 2.0     | Clocks             |

302010 rows × 20 columns

To work on the E-Commerce dataset, we need to understand two things that we will use in our analysis.

{% stepper %}
{% step %}
### To find Unique Values in a single Column

As you can see there are 302,010 rows in the dataset, but customers repeat. To find unique customers use `unique` or `nunique`.

```python
df['Customer_ID'].unique()
```

Out\[5]:

```
array([37249., 69749., 30192., ..., 49840., 58286., 29845.], shape=(86767,))
```

```python
df['Customer_ID'].nunique()
```

Out\[6]:

```
86766
```

There are 86,766 unique customers in this dataset.

A real example: Suppose you want to find Country-wise Number of Customers. If you count rows per country you will double-count customers who appear multiple times. Use `nunique` to count unique customers per country.

Wrong approach (counts rows, not unique customers):

```python
country_customer_count = df.groupby('Country').agg(
    customer_count = ('Customer_ID', 'count')
)
country_customer_count
```

Out\[7]:

| Country   | customer\_count |
| --------- | --------------- |
| Australia | 45282           |
| Canada    | 45252           |
| Germany   | 52774           |
| UK        | 63002           |
| USA       | 95122           |

Right approach (unique customers per country):

```python
country_customer_count = df.groupby('Country').agg(
    customer_count = ('Customer_ID', 'nunique')
)
country_customer_count
```

Out\[8]:

| Country   | customer\_count |
| --------- | --------------- |
| Australia | 35430           |
| Canada    | 35169           |
| Germany   | 39625           |
| UK        | 45034           |
| USA       | 58466           |
{% endstep %}

{% step %}
### Create an Age Group Column

To bucket ages into groups (10–20, 20–30, etc.) use `pd.cut`:

```python
df['Age_Group'] = pd.cut(df['Age'], bins=np.arange(10, 101, 10))
df
```

Sample output (Age\_Group column shown):

|        | Customer\_ID | Age  | ... | products           | Age\_Group |
| ------ | ------------ | ---- | --- | ------------------ | ---------- |
| 0      | 37249.0      | 21.0 | ... | Cycling shorts     | (20, 30]   |
| 1      | 69749.0      | 19.0 | ... | Lenovo Tab         | (10, 20]   |
| 2      | 30192.0      | 48.0 | ... | Sports equipment   | (40, 50]   |
| 3      | 62101.0      | 56.0 | ... | Utility knife      | (50, 60]   |
| 4      | 27901.0      | 22.0 | ... | Chocolate cookies  | (20, 30]   |
| ...    | ...          | ...  | ... | ...                | ...        |
| 302005 | 12104.0      | 31.0 | ... | Historical fiction | (30, 40]   |
| 302006 | 69772.0      | 35.0 | ... | LG Gram            | (30, 40]   |
| 302007 | 28449.0      | 41.0 | ... | Parka              | (40, 50]   |
| 302008 | 45477.0      | 41.0 | ... | TV stand           | (40, 50]   |
| 302009 | 53626.0      | 28.0 | ... | Clocks             | (20, 30]   |
{% endstep %}
{% endstepper %}

***

## Which customer segment generates the highest total revenue?

Create a Total\_Amount column and aggregate by Customer\_Segment.

```python
df['Total_Amount'] = df['Amount'] * df['Total_Purchases']

customer_segment_revenue = df.groupby('Customer_Segment').agg(
    revenue = ('Total_Amount', 'sum')
)
customer_segment_revenue = customer_segment_revenue.sort_values('revenue', ascending=False)
customer_segment_revenue
```

Out\[10]:

| Customer\_Segment | revenue      |
| ----------------- | ------------ |
| Regular           | 1.997659e+08 |
| New               | 1.244222e+08 |
| Premium           | 8.757099e+07 |

Convert to percentage:

```python
total_revenue = customer_segment_revenue['revenue'].sum()
customer_segment_revenue['per'] = customer_segment_revenue['revenue'] / total_revenue * 100
customer_segment_revenue
```

Out\[11]:

| Customer\_Segment |      revenue |       per |
| ----------------- | -----------: | --------: |
| Regular           | 1.997659e+08 | 48.515233 |
| New               | 1.244222e+08 | 30.217239 |
| Premium           | 8.757099e+07 | 21.267528 |

{% hint style="info" %}
Insight: 49% of revenue comes from Regular customers.
{% endhint %}

***

## Which customer segment generates the highest revenue per user (ARPC)?

ARPC = Total Revenue / Unique Customers.

Overall ARPC:

```python
total_revenue = df['Total_Amount'].sum()
unique_Customer = df['Customer_ID'].nunique()
arpc = total_revenue / unique_Customer
arpc
```

Out\[12]:

```
np.float64(4749.413929779314)
```

ARPC per customer segment:

```python
cdf = df.groupby('Customer_Segment').agg(
    total_revenue = ('Total_Amount', 'sum'),
    unique_Customer = ('Customer_ID', 'nunique')
)
cdf['arpc'] = cdf['total_revenue'] / cdf['unique_Customer']
cdf = cdf.sort_values('arpc', ascending=False)
cdf
```

Out\[14]:

| Customer\_Segment | total\_revenue | unique\_Customer |        arpc |
| ----------------- | -------------: | ---------------: | ----------: |
| Regular           |   1.997659e+08 |            72209 | 2766.496020 |
| New               |   1.244222e+08 |            57109 | 2178.680166 |
| Premium           |   8.757099e+07 |            45549 | 1922.566707 |

{% hint style="info" %}
Insight: Highest ARPC is Regular (≈2,766) and lowest is Premium (≈1,923).
{% endhint %}

***

## Which product category has the highest sales volume?

Sales volume = total units purchased (sum of Total\_Purchases).

```python
product_sales_vol = df.groupby('Product_Category').agg(
    sale_volume = ('Total_Purchases', 'sum')
)
product_sales_vol = product_sales_vol.sort_values('sale_volume', ascending=False)
product_sales_vol
```

Out\[15]:

| Product\_Category | sale\_volume |
| ----------------- | -----------: |
| Electronics       |     381410.0 |
| Grocery           |     357248.0 |
| Clothing          |     293529.0 |
| Books             |     292075.0 |
| Home Decor        |     291014.0 |

{% hint style="info" %}
Insight: Electronics has the highest sales volume.
{% endhint %}

***

## Which product category generates the highest revenue?

```python
product_revenue = df.groupby('Product_Category').agg(
    revenue = ('Total_Amount', 'sum'),
)
product_revenue = product_revenue.sort_values('revenue', ascending=False)
product_revenue
```

Out\[16]:

| Product\_Category |      revenue |
| ----------------- | -----------: |
| Electronics       | 9.728525e+07 |
| Grocery           | 9.096255e+07 |
| Clothing          | 7.473945e+07 |
| Books             | 7.454330e+07 |
| Home Decor        | 7.417653e+07 |

{% hint style="info" %}
Insight: Electronics has the highest revenue.
{% endhint %}

***

## Which category has the highest AOV?

AOV (Average Order Value) — different definitions shown below.

Per-row AOV (Amount per purchase):

```python
df['AOV'] = df['Amount'] / df['Total_Purchases']
df['AOV'].mean()
```

Out\[17]:

```
np.float64(77.15064527254084)
```

Overall AOV (total revenue / total orders):

```python
df['Total_Amount'].sum() / df['Total_Purchases'].sum()
```

Out\[18]:

```
np.float64(254.88533467381427)
```

AOV by Product\_Category:

```python
pdf = df.groupby('Product_Category').agg(
    revenue = ('Total_Amount', 'sum'),
    orders = ('Total_Purchases', 'sum')
)
pdf['aov'] = pdf['revenue'] / pdf['orders']
pdf = pdf.sort_values('aov', ascending=False)
pdf
```

Out\[19]:

| Product\_Category |      revenue |   orders |        aov |
| ----------------- | -----------: | -------: | ---------: |
| Books             | 7.454330e+07 | 292075.0 | 255.219728 |
| Electronics       | 9.728525e+07 | 381410.0 | 255.067380 |
| Home Decor        | 7.417653e+07 | 291014.0 | 254.889899 |
| Clothing          | 7.473945e+07 | 293529.0 | 254.623718 |
| Grocery           | 9.096255e+07 | 357248.0 | 254.620185 |

{% hint style="info" %}
Insight: Books have the highest average order value.
{% endhint %}

***

## Which category receives the best feedback (Excellent %)?

Compute count of "Excellent" per category, total feedback per category, then percentage.

```python
excellent_df = df.loc[df['Feedback'] == 'Excellent']
excellent_per_category = excellent_df.groupby('Product_Category').agg(
    excellent_count = ('Feedback', 'count')
)

total_df = df.groupby('Product_Category').agg(
    total_count = ('Feedback', 'count')
)

excellent_per_category['per'] = excellent_per_category['excellent_count'] / total_df['total_count'] * 100
excellent_per_category
```

Out\[22]:

| Product\_Category | excellent\_count |       per |
| ----------------- | ---------------: | --------: |
| Books             |            19187 | 35.150038 |
| Clothing          |            19183 | 35.065624 |
| Electronics       |            24028 | 33.769483 |
| Grocery           |            19268 | 28.863756 |
| Home Decor        |            18980 | 34.926301 |

***

## Which category has the highest and lowest average rating?

```python
category_rating = df.groupby('Product_Category').agg(
    avg_rating = ('Ratings', 'mean'),
    median_rating = ('Ratings', 'median')
)
category_rating
```

Out\[23]:

| Product\_Category | avg\_rating | median\_rating |
| ----------------- | ----------: | -------------: |
| Books             |    3.112428 |            3.0 |
| Clothing          |    3.104266 |            3.0 |
| Electronics       |    3.268857 |            4.0 |
| Grocery           |    3.181739 |            3.0 |
| Home Decor        |    3.109600 |            3.0 |

***

## Which product category has the highest return on each customer?

highest return = revenue / unique customer

```python
pdf = df.groupby('Product_Category').agg(
    revenue = ('Total_Amount', 'sum'),
    customer_count = ('Customer_ID', 'nunique')
)
pdf['highest return'] = pdf['revenue'] / pdf['customer_count']
pdf = pdf.sort_values('highest return', ascending=False)
pdf
```

Out\[24]:

| Product\_Category |      revenue | customer\_count | highest return |
| ----------------- | -----------: | --------------: | -------------: |
| Electronics       | 9.728525e+07 |           48945 |    1987.644285 |
| Grocery           | 9.096255e+07 |           46823 |    1942.689529 |
| Clothing          | 7.473945e+07 |           40770 |    1833.197086 |
| Home Decor        | 7.417653e+07 |           40530 |    1830.163560 |
| Books             | 7.454330e+07 |           40803 |    1826.907389 |

***

## Which category has the highest ARPU?

ARPU = Revenue / Total Orders (orders counted as Total\_Purchases sum)

```python
adf = df.groupby('Product_Category').agg(
    revenue = ('Total_Amount', 'sum'),
    total_order = ('Total_Purchases', 'sum')
)
adf['aov'] = adf['revenue'] / adf['total_order']
adf
```

Out\[27]:

| Product\_Category |      revenue | total\_order |         aov |
| ----------------- | -----------: | -----------: | ----------: |
| Books             | 7.454330e+07 |        54572 | 1365.962439 |
| Clothing          | 7.473945e+07 |        54659 | 1367.376739 |
| Electronics       | 9.728525e+07 |        71121 | 1367.883600 |
| Grocery           | 9.096255e+07 |        66708 | 1363.592850 |
| Home Decor        | 7.417653e+07 |        54306 | 1365.899332 |

***

## Which category has the highest AOV? (alternate calculation)

AOV = Revenue / Number of Orders (counting orders as rows)

```python
adf = df.groupby('Product_Category').agg(
    revenue = ('Total_Amount', 'sum'),
    total_order = ('Total_Purchases', 'count')
)
adf['aov'] = adf['revenue'] / adf['total_order']
adf
```

Out\[28]:

| Product\_Category |      revenue | total\_order |         aov |
| ----------------- | -----------: | -----------: | ----------: |
| Books             | 7.454330e+07 |        54572 | 1365.962439 |
| Clothing          | 7.473945e+07 |        54659 | 1367.376739 |
| Electronics       | 9.728525e+07 |        71121 | 1367.883600 |
| Grocery           | 9.096255e+07 |        66708 | 1363.592850 |
| Home Decor        | 7.417653e+07 |        54306 | 1365.899332 |

***

(End of analysis)
