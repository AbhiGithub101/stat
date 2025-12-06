# Data Cleaning in Pandas

## Duplicacy and Missing Values

When working with data, you'll often encounter duplicate records or missing values. This guide shows how to find and handle them using pandas.

```python
import pandas as pd
```

### Sample dataset (duplicates)

```python
df = pd.read_csv('duplicate dataset.csv')
df
```

|    | CustomerID | CustomerName    | Email                  | Phone      | City   | SignupDate |
| -- | ---------- | --------------- | ---------------------- | ---------- | ------ | ---------- |
| 0  | C001       | Abhishek Mishra | abhishek@gmail.com     | 9876543210 | Kanpur | 2024-01-05 |
| 1  | C002       | Riya Sharma     | riya.sharma@gmail.com  | 9123456780 | Delhi  | 2024-01-07 |
| 2  | C003       | Arjun Verma     | arjun.verma@gmail.com  | 9988776655 | Mumbai | 2024-01-10 |
| 3  | C004       | Neha Agarwal    | neha.agrawal@gmail.com | 9090909090 | Pune   | 2024-01-11 |
| 4  | C005       | Sunil Mehra     | sunil.mehra@gmail.com  | 9876501234 | Kanpur | 2024-01-12 |
| 5  | C001       | Abhishek Mishra | abhishek@gmail.com     | 9876543210 | Kanpur | 2024-01-05 |
| 6  | C001       | Abhishek Mishra | abhishek@gmail.com     | 9876543210 | Kanpur | 2024-01-05 |
| 7  | C002       | Riya Sharma     | riya.sharma@gmail.com  | 9123456780 | Delhi  | 2024-01-07 |
| 8  | C003       | Arjun Verma     | arjun.verma@gmail.com  | 9988776600 | Mumbai | 2024-01-10 |
| 9  | C004       | Neha Agarwal    | neha.a@gmail.com       | 9090909090 | Pune   | 2024-01-11 |
| 10 | C006       | Sunil Kumar     | sunil.mehra@gmail.com  | 9876511111 | Kanpur | 2024-01-12 |
| 11 | C007       | Meera Singh     | meera.singh@gmail.com  | 9876543210 | Delhi  | 2024-01-15 |
| 12 | C008       | Rohan Singh     | rohan@gmail.com        | 9876501234 | Kanpur | 2024-01-20 |
| 13 | C009       | Sunita Sharma   | sunil.mehra@gmail.com  | 9999999999 | Mumbai | 2024-01-21 |
| 14 | C010       | Amit Tandon     | amit@gmail.com         | 9123456780 | Pune   | 2024-01-22 |

### How to find exact duplicate rows

Use `duplicated()` with `loc` to filter duplicate rows:

```python
df.loc[df.duplicated()]
```

Output:

|   | CustomerID | CustomerName    | Email                 | Phone      | City   | SignupDate |
| - | ---------- | --------------- | --------------------- | ---------- | ------ | ---------- |
| 5 | C001       | Abhishek Mishra | abhishek@gmail.com    | 9876543210 | Kanpur | 2024-01-05 |
| 6 | C001       | Abhishek Mishra | abhishek@gmail.com    | 9876543210 | Kanpur | 2024-01-05 |
| 7 | C002       | Riya Sharma     | riya.sharma@gmail.com | 9123456780 | Delhi  | 2024-01-07 |

Note: The `keep` parameter controls which duplicates are considered duplicates.

{% stepper %}
{% step %}
### keep parameter — options

* keep='first' — does not consider the first occurrence as duplicate
* keep='last' — does not consider the last occurrence as duplicate
* keep=False — considers all duplicate rows as duplicates

Examples:

```python
df.loc[df.duplicated(keep='first')]
```

```python
df.loc[df.duplicated(keep='last')]
```

```python
df.loc[df.duplicated(keep=False)]
```
{% endstep %}
{% endstepper %}

### subset parameter

`subset` helps find duplicates considering only selected column(s):

```python
df.loc[df.duplicated(subset='Email', keep=False)]
```

Example output (duplicates by Email):

|    | CustomerID | CustomerName    | Email                 | Phone      | City   | SignupDate |
| -- | ---------- | --------------- | --------------------- | ---------- | ------ | ---------- |
| 0  | C001       | Abhishek Mishra | abhishek@gmail.com    | 9876543210 | Kanpur | 2024-01-05 |
| 1  | C002       | Riya Sharma     | riya.sharma@gmail.com | 9123456780 | Delhi  | 2024-01-07 |
| 2  | C003       | Arjun Verma     | arjun.verma@gmail.com | 9988776655 | Mumbai | 2024-01-10 |
| 4  | C005       | Sunil Mehra     | sunil.mehra@gmail.com | 9876501234 | Kanpur | 2024-01-12 |
| 5  | C001       | Abhishek Mishra | abhishek@gmail.com    | 9876543210 | Kanpur | 2024-01-05 |
| 6  | C001       | Abhishek Mishra | abhishek@gmail.com    | 9876543210 | Kanpur | 2024-01-05 |
| 7  | C002       | Riya Sharma     | riya.sharma@gmail.com | 9123456780 | Delhi  | 2024-01-07 |
| 8  | C003       | Arjun Verma     | arjun.verma@gmail.com | 9988776600 | Mumbai | 2024-01-10 |
| 10 | C006       | Sunil Kumar     | sunil.mehra@gmail.com | 9876511111 | Kanpur | 2024-01-12 |
| 13 | C009       | Sunita Sharma   | sunil.mehra@gmail.com | 9999999999 | Mumbai | 2024-01-21 |

#### Example: find records where Name and City are same

```python
df.loc[df.duplicated(subset=['CustomerName','City'], keep=False)]
```

### drop\_duplicates()

Drop duplicates with `drop_duplicates()`:

```python
df = df.drop_duplicates()
df
```

Output (after dropping exact duplicate rows):

|    | CustomerID | CustomerName    | Email                  | Phone      | City   | SignupDate |
| -- | ---------- | --------------- | ---------------------- | ---------- | ------ | ---------- |
| 0  | C001       | Abhishek Mishra | abhishek@gmail.com     | 9876543210 | Kanpur | 2024-01-05 |
| 1  | C002       | Riya Sharma     | riya.sharma@gmail.com  | 9123456780 | Delhi  | 2024-01-07 |
| 2  | C003       | Arjun Verma     | arjun.verma@gmail.com  | 9988776655 | Mumbai | 2024-01-10 |
| 3  | C004       | Neha Agarwal    | neha.agrawal@gmail.com | 9090909090 | Pune   | 2024-01-11 |
| 4  | C005       | Sunil Mehra     | sunil.mehra@gmail.com  | 9876501234 | Kanpur | 2024-01-12 |
| 8  | C003       | Arjun Verma     | arjun.verma@gmail.com  | 9988776600 | Mumbai | 2024-01-10 |
| 9  | C004       | Neha Agarwal    | neha.a@gmail.com       | 9090909090 | Pune   | 2024-01-11 |
| 10 | C006       | Sunil Kumar     | sunil.mehra@gmail.com  | 9876511111 | Kanpur | 2024-01-12 |
| 11 | C007       | Meera Singh     | meera.singh@gmail.com  | 9876543210 | Delhi  | 2024-01-15 |
| 12 | C008       | Rohan Singh     | rohan@gmail.com        | 9876501234 | Kanpur | 2024-01-20 |
| 13 | C009       | Sunita Sharma   | sunil.mehra@gmail.com  | 9999999999 | Mumbai | 2024-01-21 |
| 14 | C010       | Amit Tandon     | amit@gmail.com         | 9123456780 | Pune   | 2024-01-22 |

Example: delete rows where Phone is same (possible fraud case):

```python
df = df.drop_duplicates(subset='Phone', keep=False)
df
```

Example: delete rows where Phone and Email are same:

```python
df = df.drop_duplicates(subset=['Email','Phone'], keep=False)
df
```

Combining steps to clean the data (example workflow provided in original content):

* Re-read CSV
* drop exact duplicates
* drop duplicates by Email or Phone as needed

(See original code examples for exact sequences and outputs.)

***

## Missing Value in Pandas

Missing values must be handled because they can break calculations, introduce bias, or cause errors in analysis and models. The examples below use a sample CSV called `missing file.csv`.

```python
df = pd.read_csv('missing file.csv')
df
```

|    | CustomerID | Name         | Age  | City      | Email             | PurchaseAmount |
| -- | ---------- | ------------ | ---- | --------- | ----------------- | -------------- |
| 0  | c001       | Rahul Sharma | 28.0 | Delhi     | rahul@example.com | 1200.0         |
| 1  | c002       | Priya Singh  | NaN  | Mumbai    | priya@example.com | 1500.0         |
| 2  | NaN        | NaN          | NaN  | NaN       | NaN               | NaN            |
| 3  | c003       | Amit Verma   | 35.0 | NaN       | amit@example.com  | NaN            |
| 4  | c004       | NaN          | 42.0 | Pune      | NaN               | 2000.0         |
| 5  | c005       | Neha Rao     | 30.0 | Bangalore | neha@example.com  | 1800.0         |
| 6  | NaN        | NaN          | NaN  | NaN       | NaN               | NaN            |
| 7  | c006       | Ravi Kumar   | NaN  | Chennai   | ravi@example.com  | NaN            |
| 8  | c007       | NaN          | 25.0 | NaN       | NaN               | NaN            |
| 9  | c008       | Sonia Mehra  | 29.0 | Delhi     | sonia@example.com | 1600.0         |
| 10 | NaN        | NaN          | NaN  | NaN       | NaN               | NaN            |

### isna() / isnull()

`isna()`/`isnull()` indicate missing values (True if missing):

```python
df.isna()
```

Output (boolean mask) — see original output table.

### isna().sum() / isnull().sum()

Count missing per column:

```python
df.isnull().sum()
```

Example output:

CustomerID 3 Name 5 Age 5 City 5 Email 5 PurchaseAmount 6 dtype: int64

#### Count missing per row (axis=1)

```python
df['missing'] = df.isnull().sum(axis=1)
df
```

The `missing` column shows the number of NaNs per row (see original table).

#### Filter rows with missing in a specific column

```python
df.loc[df['Age'].isnull()]
```

### notna() / notnull()

`notna()`/`notnull()` indicate non-missing values (True if present).

```python
df = pd.read_csv('missing file.csv')
df.notna().sum()
```

Example output:

CustomerID 8 Name 6 Age 6 City 6 Email 6 PurchaseAmount 5 dtype: int64

Count non-missing per row:

```python
df['not missing'] = df.notnull().sum(axis=1)
df
```

Filter rows where Age is not missing:

```python
df.loc[df['Age'].notnull()]
```

### fillna()

`fillna()` replaces NaN values.

Common uses:

* Replace with fixed value: `df.fillna(0)`
* Replace with statistics: `df['col'].fillna(df['col'].mean())`

Example (simple fill):

```python
df = df.fillna(0)
df
```

Example using a dictionary to fill different columns differently:

```python
df = pd.read_csv('missing file.csv')
d = {
  'CustomerID': 'User',
  'Name': 'user',
  'Age': df['Age'].mean(),
  'City': 'no city',
  'Email': 'no email',
}
df = df.fillna(d)
df
```

Fill a single column with its mean:

```python
df['PurchaseAmount'] = df['PurchaseAmount'].fillna(df['PurchaseAmount'].mean())
df
```

### dropna()

`dropna()` removes rows or columns with NaN.

When to use:

* If missing values are few and can be removed without harming analysis.
* When you need fully complete records.

#### how parameter

* how='any' — drop if any NaN in row/column
* how='all' — drop only if all values are NaN

Examples:

```python
# delete rows if any value is missing
df = df.dropna(how='any')
```

```python
# delete rows if all values are missing
df = df.dropna(how='all')
```

#### subset parameter

Check only specific columns when deciding to drop rows:

```python
df = df.dropna(subset=['Email', 'Phone'])
```

This drops rows where Email OR Phone is missing (depending on `how`).

Examples:

```python
# delete rows where Age is missing
df = df.dropna(subset='Age')

# delete rows where Name OR City (anything) is missing
df = df.dropna(subset=['Name','City'])
# default how='any' so it removes rows missing in any of those columns

# delete rows where Name, Age, City all are missing
df = df.dropna(subset=['Name','Age','City'], how='all')
```

#### thresh parameter

`thresh` sets the minimum number of non-NaN values required to keep a row.

```python
# keep rows with at least 3 non-null values
df = df.dropna(thresh=3)
```

or restrict to subset:

```python
# keep rows where at least 2 of Name,Age,City are present
df = df.dropna(subset=['Name','Age','City'], thresh=2)
```

***

{% stepper %}
{% step %}
## Assignments — Practical Questions on Handling Missing Values

### 1. Missing Value Checks

* Write code to check how many missing values each column has.
* Add a new column `"missing"` that counts missing values row-wise.

(Use `df.isnull().sum()` and `df['missing'] = df.isnull().sum(axis=1)`.)
{% endstep %}

{% step %}
### 2. dropna() Practice

* Drop all rows that contain any missing value.
* Drop all rows that contain only missing values.
* Drop rows where the Email column is missing.
* Drop rows where Name OR City is missing.
* Drop rows where Name AND Email are missing using `subset`.
* Keep only those rows that have at least 3 non-missing values (use `thresh`).

(Use `df.dropna()` with `how`, `subset`, and `thresh` as shown above.)
{% endstep %}

{% step %}
### 3. fillna() Practice

* Fill missing values in City with `"Unknown"`.
* Fill missing numeric values in "Age" with the mean.
* Fill missing numeric values in "Salary" with the median.
* Fill missing values of "Phone" with `"Not Provided"`.
* Fill missing Email values with `"test@example.com"`.

(Use `df['City'] = df['City'].fillna('Unknown')`, `df['Age'].fillna(df['Age'].mean())`, etc.)
{% endstep %}

{% step %}
### 4. subset Parameter Practice

* Drop rows where Email and Phone are missing using `subset`.
* Drop rows where SignupDate is missing.

(Use `df.dropna(subset=['Email','Phone'])` and `df.dropna(subset=['SignupDate'])`.)
{% endstep %}

{% step %}
### 5. Custom Practical Tasks

* Create a new DataFrame keeping only rows where at least 2 columns have values.
* Fill missing values in "City" with `"NA"`.
* Replace missing "Age" values with 0.
* Replace all missing values in the entire DataFrame with `"Missing"`.
* Fill missing values only in numeric columns using their mean.

(Use `dropna(thresh=2)`, `fillna()`, `select_dtypes(include=[np.number])` etc.)
{% endstep %}
{% endstepper %}

***

If you want, I can convert any of the code snippets into ready-to-run, copy-paste Python cells, or provide a compact clean-up pipeline that combines duplicate removal and missing-value handling for your specific dataset. Which would you prefer?
