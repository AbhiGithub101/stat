# UDF

UDF (user-defined function) is a function written by the user to apply custom logic on your data.\
It is used when there is no built-in function and you need to create a function.

```python
import pandas as pd

df = pd.read_csv('score.csv')
df['total'] = df.iloc[:, 1:6].sum(axis=1)
df.head()
```

Output:

|    | Name    | Math | Science | English | History | Art | total |
| -: | ------- | ---: | ------: | ------: | ------: | --: | ----: |
|  0 | Alice   |   78 |      82 |      75 |      68 |  90 |   393 |
|  1 | Bob     |   85 |      79 |      80 |      74 |  87 |   405 |
|  2 | Charlie |   92 |      95 |      85 |      89 |  93 |   454 |
|  3 | David   |   65 |      70 |      60 |      55 |  72 |   322 |
|  4 | Eva     |   88 |      90 |      78 |      82 |  85 |   423 |

## Create a column Grade

Grading logic:

* A : if mark is greater than 450
* B : if mark is greater than 350
* C : if mark is less than 350

### Create a function for this column

```python
def myf(v):
    if v >= 450:
        return 'A'
    elif v >= 350:
        return 'B'
    else:
        return 'C'
```



### Applying this function on total Column

```python
df['Grade'] = df['total'].apply(myf)
df.head()
```

Output:

|    | Name    | Math | Science | English | History | Art | total | Grade |
| -: | ------- | ---: | ------: | ------: | ------: | --: | ----: | :---: |
|  0 | Alice   |   78 |      82 |      75 |      68 |  90 |   393 |   B   |
|  1 | Bob     |   85 |      79 |      80 |      74 |  87 |   405 |   B   |
|  2 | Charlie |   92 |      95 |      85 |      89 |  93 |   454 |   A   |
|  3 | David   |   65 |      70 |      60 |      55 |  72 |   322 |   C   |
|  4 | Eva     |   88 |      90 |      78 |      82 |  85 |   423 |   B   |
|    |         |      |         |         |         |     |       |       |

### Use Case 1 : India Quarter

In Which Quarter did we have the most expense ?

In india, quarter are defined as :&#x20;

```

US            IN
2- Apr - Jun = 1
3- Jul - Sep = 2
4- Oct - Dec = 3
1- Jan - Mar = 4
```

```python
df = pd.read_csv('expense.csv')
df.head()
```

Output:

|    | date       | amount | category    |
| -: | ---------- | -----: | ----------- |
|  0 | 03/01/2024 |    520 | Groceries   |
|  1 | 07/01/2024 |    150 | Transport   |
|  2 | 15/01/2024 |    980 | Electronics |
|  3 | 28/01/2024 |    220 | Dining      |
|  4 | 05/02/2024 |    430 | Rent        |

Convert to datetime and get pandas quarter:

```python
df['date'] = pd.to_datetime(df['date'], format='%d/%m/%Y')
df.head()
```

Output:

|    | date       | amount | category    |
| -: | ---------- | -----: | ----------- |
|  0 | 2024-01-03 |    520 | Groceries   |
|  1 | 2024-01-07 |    150 | Transport   |
|  2 | 2024-01-15 |    980 | Electronics |
|  3 | 2024-01-28 |    220 | Dining      |
|  4 | 2024-02-05 |    430 | Rent        |

Get pandas quarter:

```python
df['uq'] = df['date'].dt.quarter
df.head()
```

Output:

|    | date       | amount | category    | uq |
| -: | ---------- | -----: | ----------- | -: |
|  0 | 2024-01-03 |    520 | Groceries   |  1 |
|  1 | 2024-01-07 |    150 | Transport   |  1 |
|  2 | 2024-01-15 |    980 | Electronics |  1 |
|  3 | 2024-01-28 |    220 | Dining      |  1 |
|  4 | 2024-02-05 |    430 | Rent        |  1 |

Create function to convert pandas quarter to Indian quarter:

```python
def iq(v):
    if v == 1:
        return 4
    elif v == 2:
        return 1
    elif v == 3:
        return 2
    else:
        return 3
```

Apply it:

```python
df['india_q'] = df['uq'].apply(iq)
df.head()
```

Output:

|    | date       | amount | category    | uq | india\_q |
| -: | ---------- | -----: | ----------- | -: | -------: |
|  0 | 2024-01-03 |    520 | Groceries   |  1 |        4 |
|  1 | 2024-01-07 |    150 | Transport   |  1 |        4 |
|  2 | 2024-01-15 |    980 | Electronics |  1 |        4 |
|  3 | 2024-01-28 |    220 | Dining      |  1 |        4 |
|  4 | 2024-02-05 |    430 | Rent        |  1 |        4 |

Aggregate totals by Indian quarter and sort descending:

```python
mdf = df.groupby('india_q').agg(total=('amount', 'sum'))
mdf = mdf.sort_values('total', ascending=False)
mdf
```

Output:

| india\_q | total |
| -------: | ----: |
|        4 |  7190 |
|        2 |  6170 |
|        1 |  4345 |
|        3 |  3020 |

***

## Use Case 2: Age Group

Q: Which age group purchases from us the most?

Load retail dataset:

```python
df = pd.read_csv('retail_sales_dataset.csv')
df.head()
```

Output:

|    | Customer ID | Gender | Age | Product Category | Quantity | Price per Unit |
| -: | ----------- | ------ | --: | ---------------- | -------: | -------------: |
|  0 | CUST001     | Male   |  34 | Beauty           |        3 |             50 |
|  1 | CUST002     | Female |  26 | Clothing         |        2 |            500 |
|  2 | CUST003     | Male   |  50 | Electronics      |        1 |             30 |
|  3 | CUST004     | Male   |  37 | Clothing         |        1 |            500 |
|  4 | CUST005     | Male   |  30 | Beauty           |        2 |             50 |

Create function that returns age group:

```python
def myf(v):
    if v >= 0 and v < 10:
        return '0-10'
    elif v >= 10 and v < 20:
        return '10-20'
    elif v >= 20 and v < 30:
        return '20-30'
    elif v >= 30 and v < 40:
        return '30-40'
    elif v >= 40 and v < 50:
        return '40-50'
    elif v >= 50 and v < 60:
        return '50-60'
    elif v >= 60 and v < 70:
        return '60-70'
    elif v >= 70 and v < 80:
        return '70-80'
    else:
        return '80+'
```

Apply it:

```python
df['age group'] = df['Age'].apply(myf)
df.head()
```

Output:

|    | Customer ID | Gender | Age | Product Category | Quantity | Price per Unit | age group |
| -: | ----------- | ------ | --: | ---------------- | -------: | -------------: | :-------: |
|  0 | CUST001     | Male   |  34 | Beauty           |        3 |             50 |   30-40   |
|  1 | CUST002     | Female |  26 | Clothing         |        2 |            500 |   20-30   |
|  2 | CUST003     | Male   |  50 | Electronics      |        1 |             30 |   50-60   |
|  3 | CUST004     | Male   |  37 | Clothing         |        1 |            500 |   30-40   |
|  4 | CUST005     | Male   |  30 | Beauty           |        2 |             50 |   30-40   |

Count age groups:

```python
df['age group'].value_counts()
```

Output:

age group counts:

* 40-50 222
* 50-60 221
* 20-30 209
* 30-40 191
* 60-70 115
* 10-20 42

***

## Review - Language Conversion

Sometimes we need an external module to be applied on a whole column. In that scenario, we can use a function to apply that module to the whole column.

Example using deep\_translator (install with pip install deep\_translator).

Load reviews:

```python
df = pd.read_csv('review in language.csv')
df
```

Output:

|    | id | review                                     | rating |
| -: | -- | ------------------------------------------ | -----: |
|  0 | 1  | This product is very good and useful       |      5 |
|  1 | 2  | यह प्रोडक्ट बहुत बढ़िया है और किफायती भी।  |      4 |
|  2 | 3  | I am not satisfied with the quality        |      2 |
|  3 | 4  | C'est un excellent produit j'adore         |      5 |
|  4 | 5  | इसकी पैकिंग खराब थी लेकिन प्रोडक्ट ठीक था। |      3 |

Simple example of conversion with GoogleTranslator:

```python
from deep_translator import GoogleTranslator

review = "this is good product."
translation = GoogleTranslator(source='auto', target='hi').translate(review)
print(translation)
```

Output: यह अच्छा उत्पाद है.

Applying this translator to the review column:

```python
from deep_translator import GoogleTranslator

df = pd.read_csv('review in language.csv')

def trans(v):
    translation = GoogleTranslator(source='auto', target='en').translate(v)
    return translation

df['eng_review'] = df['review'].apply(trans)
df
```

Output:

|    | id | review                                     | rating | eng\_review                                   |
| -: | -- | ------------------------------------------ | -----: | --------------------------------------------- |
|  0 | 1  | This product is very good and useful       |      5 | This product is very good and useful          |
|  1 | 2  | यह प्रोडक्ट बहुत बढ़िया है और किफायती भी।  |      4 | This product is great and affordable too.     |
|  2 | 3  | I am not satisfied with the quality        |      2 | I am not satisfied with the quality           |
|  3 | 4  | C'est un excellent produit j'adore         |      5 | It's a great product I love it                |
|  4 | 5  | इसकी पैकिंग खराब थी लेकिन प्रोडक्ट ठीक था। |      3 | Its packing was bad but the product was fine. |
