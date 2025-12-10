# Outlier in pandas

## What is an Outlier?

An **outlier** is a data point that is **significantly different** from the rest of the values in a dataset. It either lies **too high** or **too low** compared to the majority of the observations.

In simple words:

* Outliers are values that **don’t fit the general pattern** of the data.
* They can occur due to **data entry errors**, **measurement mistakes**, or **genuine rare events**.
* Outliers can **distort averages**, **affect model performance**, and **mislead analysis**, so they need special attention.

Example Scenario

Suppose you are analyzing daily temperatures of a city, and most days fall between **20°C – 35°C**. If one day suddenly shows a recorded temperature of **70°C**, that value is an outlier.

Why Outliers Matter

* They affect **mean**, **standard deviation**, and **visualisation shapes**.
* They can indicate **system errors**, **sensor malfunctions**, or **special cases**.

***

### Simple Scenario

{% stepper %}
{% step %}
### Salary example — baseline

salary1 = 100 200 500
{% endstep %}

{% step %}
### Salary example — with a possible outlier

salary = 100 200 500 10000

In this scenario, the outlier is the person who has salary of 10000. We need to detect outlier(s) and remove them for some analysis.
{% endstep %}
{% endstepper %}

***

### Measure of Central Tendency

The measure of central tendency finds the center or typical value in a set of data.

Three main types:

* Mean (Average) – Add up all numbers and divide by how many there are. Example: (2 + 4 + 6) / 3 = 4
* Median – The middle value when numbers are arranged in order. Example: In \[3, 5, 8], the median is 5.
* Mode – The value that appears most often. Example: In \[2, 3, 3, 5], the mode is 3.

***

### Measure of Spread

* Range = Max - Min\
  Example: (10,20,30,40) → Range = 40 - 10 = 30

Example code (illustrative):

```python
import numpy as np
score1 = [10,20,30,70]
score2 = [0,5,4,100]
range1 = max(score1) - min(score1)
range2 = max(score2) - min(score2)
range1, range2
# Out: (60, 100)
```

***

### Variance and Standard Deviation

* Variance: how spread out numbers are from the mean.
* Standard Deviation (STD): square root of variance. We generally prefer STD because its scale is the same as the original data and is easier to interpret.

Understanding STD1, STD2, STD3 (1, 2, 3 standard deviations) is helpful to classify data points as normal, unusual, or outliers.

Empirical Rule (68-95-99.7):

* STD1: Mean ± 1 STD → \~68% of data (very normal)
* STD2: Mean ± 2 STD → \~95% of data (less common)
* STD3: Mean ± 3 STD → \~99.7% of data (rare)
* Beyond STD3 → Outliers (\~0.3% of data)

Example (Mean = 50, STD = 10):

* STD1 range: 40 to 60
* STD2 range: 30 to 70
* STD3 range: 20 to 80
* Outliers: values < 20 or > 80

***

## A Way to Find Outliers (worked example with code)

The examples below use a dataset loaded from "Adidas US Sales Datasets.xlsx". The column `total` is computed as Price per Unit \* Units Sold.

Step-by-step process (mean/std and IQR approaches):

{% stepper %}
{% step %}
### Load data and compute total

```python
import pandas as pd
import numpy as np

df = pd.read_excel('Adidas US Sales Datasets.xlsx')
df['total'] = df['Price per Unit'] * df['Units Sold']
df.shape
# Out: (9648, 10)
```

Example of first rows (truncated):

| Retailer    | Invoice Date | Region    | State    | City     | Product               | Price per Unit | Units Sold | Sales Method |   total |
| ----------- | ------------ | --------- | -------- | -------- | --------------------- | -------------: | ---------: | ------------ | ------: |
| Foot Locker | 2020-01-01   | Northeast | New York | New York | Men's Street Footwear |           50.0 |       1200 | In-store     | 60000.0 |
| ...         | ...          | ...       | ...      | ...      | ...                   |            ... |        ... | ...          |     ... |
{% endstep %}

{% step %}
### Method 1 — Mean and Standard Deviation (STD) approach

Compute mean and std:

```python
mean = df['total'].mean()
std = df['total'].std()
mean, std
# Example Out:
# mean = 12455.083955223881
# std  = 12716.3921114572
```

1-STD range:

```python
std1 = (mean - std, mean + std)
# Example Out: (-261.3081562333191, 25171.476066681083)
```

3-STD range:

```python
lv, uv = mean - 3 * std, mean + 3 * std
# Example Out: (-25694.092379147718, 50604.260289595484)
```

Filter rows within ±3 STD:

```python
odf = df.loc[df['total'].between(lv, uv)]
odf.shape
# Example Out: (9442, 10)
odf['total'].mean()
# Example Out: 11414.382546070749
```

Note: mean/std is sensitive to extreme outliers — high values inflate the mean and std.
{% endstep %}

{% step %}
### Percentiles and Quartiles (concept)

* A percentile shows the percentage of observations below a value. Example: 50th percentile = median.
* Quartiles: 25% (Q1), 50% (Q2), 75% (Q3). Most data often lies between Q1 and Q3.

Example usage:

```python
x = [10,20,30,40,50,60,70,80,90]
np.percentile(x, 50)   # median
np.percentile(x, [25,75])
# Out: array([30., 70.])
```
{% endstep %}

{% step %}
### Method 2 — IQR (Interquartile Range) method

Compute Q1 and Q3, then IQR and fences:

```python
q1, q3 = np.percentile(df['total'], [25, 75])
iqr = q3 - q1
lv = q1 - 1.5 * iqr
uv = q3 + 1.5 * iqr
q1, q3, iqr, lv, uv
# Example Out:
# q1 = 4065.25
# q3 = 15864.5
# iqr = 11799.25
# lv = -13633.625
# uv = 33563.375
```

Filter using IQR fences:

```python
odf = df.loc[df['total'].between(lv, uv)]
odf.shape
# Example Out: (8849, 10)
odf['total'].mean()
# Example Out: 9446.502429653068
```

Notes:

* IQR is robust to outliers and often preferred to find outliers in skewed data.
* Observations outside \[Q1 - 1.&#x35;_&#x49;QR, Q3 + 1.&#x35;_&#x49;QR] are commonly considered outliers.
{% endstep %}
{% endstepper %}

***

### Box plot illustration

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>



***

### Box plot IQR example (small numeric example)

Data:

```python
x = [10,20,30,40,50,60,70,80,90]
```

Find Q1 and Q3:

```python
q1,q3 = np.percentile(x,[25,75])
# q1 = 30.0, q3 = 70.0
```

IQR:

```python
iqr = q3 - q1  # 40.0
```

Fences:

```python
lv = q1 - 1.5 * iqr   # -30.0
uv = q3 + 1.5 * iqr   # 130.0
```

Note: Not every dataset will contain outliers; fences indicate where outliers would lie.

***

### Summary: Which method to pick?

* Use IQR when you want a robust method less affected by extreme values (good for skewed distributions).



