# Outlier in pandas

## What is an Outlier?

An **outlier** is a data point that is **significantly different** from the rest of the values in a dataset — either much higher or much lower than the majority of observations.

* Outliers are values that **don’t fit the general pattern** of the data.
* They can occur because of **data entry errors**, **measurement mistakes**, or **genuine rare events**.
* Outliers can **distort averages**, **affect model performance**, and **mislead analysis**, so they need special attention.

Example: If daily temperatures are normally between 20°C–35°C and one day shows 70°C, that is an outlier.

Why outliers matter

* They affect **mean**, **standard deviation**, and visualization shapes.
* They can indicate **system errors**, **sensor malfunctions**, or **special cases**.

***

### Simple Scenario

salary1 = 100 200 500\
salary = 100 200 500 10000

Here, the outlier is the salary of 10000. We may need to detect and remove it for certain analyses.

***

### Measures of Central Tendency

Ways to find the "center" of data:

* Mean (average)
* Median (middle value)
* Mode (most frequent value)

***

### Measure of Spread

* Range = Max - Min

Example (in Python style):

```python
score1 = [10, 20, 30, 70]
score2 = [0, 5, 4, 100]
range1 = max(score1) - min(score1)
range2 = max(score2) - min(score2)
range1, range2  # (60, 100)
```

***

### Variance and Standard Deviation

* Variance: how spread out numbers are from the mean.
* Standard deviation (STD): square root of variance — often used because it's in the same units as the data.

Understanding STD1, STD2, STD3:

* STD1: mean ± 1 STD → \~68% of data
* STD2: mean ± 2 STD → \~95% of data
* STD3: mean ± 3 STD → \~99.7% of data

Empirical Rule (68-95-99.7):

| Range       | Meaning         | % of Data       |
| ----------- | --------------- | --------------- |
| STD1        | Mean ± 1 STD    | 68%             |
| STD2        | Mean ± 2 STD    | 95%             |
| STD3        | Mean ± 3 STD    | 99.7%           |
| Beyond STD3 | Outside ± 3 STD | 0.3% (outliers) |

Example:

* Mean = 50, STD = 10
  * STD1: 40–60
  * STD2: 30–70
  * STD3: 20–80
  * Outliers: <20 or >80

***

## A Way to Find Outliers (Applied Example with a Sales Dataset)

We work with an "Adidas US Sales Datasets.xlsx" and add a `total` column:

```python
import pandas as pd
import numpy as np

df = pd.read_excel('Adidas US Sales Datasets.xlsx')
df['total'] = df['Price per Unit'] * df['Units Sold']
df.shape  # 9648 rows × 10 columns
```

Find average sales amount:

```python
df['total'].mean()
# np.float64(12455.083955223881)
```

Your manager says the average is too big — we should check for outliers and remove them.

***

### Outlier detection by Standard Deviation (example)

Compute mean and std, then find ±1 STD and ±3 STD ranges:

```python
mean = df['total'].mean()
std = df['total'].std()

std1 = (mean - std, mean + std)
# (-261.3081562333191, 25171.476066681083)

lv, uv = mean - 3 * std, mean + 3 * std
# (-25694.092379147718, 50604.260289595484)
```

Filter between ±3 STD:

```python
odf = df.loc[df['total'].between(lv, uv)]
odf.shape  # 9442 rows × 10 columns

odf['total'].mean()
# np.float64(11414.382546070749)
```

Note: Using ±3 STD removed some extreme values and reduced the mean.

***

### Another way: Percentiles and Quartiles

* Percentile: divides data into 100 parts. The 50th percentile = median.
* Quartiles: 25% (Q1), 50% (Q2), 75% (Q3).

Example:

```python
x = [10,20,30,40,50,60,70,80,90]
np.percentile(x, 50)  # 50th percentile (median)
np.percentile(x, [25, 75])
# array([30., 70.])
```

***

### Box Plot (visual method)

(image embedded in original content — left as-is)

(This is a base64 image — preserved.)

***

## Using the IQR Method to Find Outliers

We’ll use the IQR method (boxplot rule) for outlier detection:

* Compute Q1 (25th percentile) and Q3 (75th percentile).
* IQR = Q3 - Q1
* Lower bound = Q1 - 1.5 \* IQR
* Upper bound = Q3 + 1.5 \* IQR
* Points outside \[lower bound, upper bound] are considered outliers.

{% stepper %}
{% step %}
### Step 1 — Example (simple list)

```python
x = [10,20,30,40,50,60,70,80,90]
q1, q3 = np.percentile(x, [25, 75])
# q1 = 30.0, q3 = 70.0

iqr = q3 - q1  # 40.0

lv = q1 - 1.5 * iqr  # -30.0
uv = q3 + 1.5 * iqr  # 130.0
# No outliers in x since all values are between -30 and 130
```
{% endstep %}

{% step %}
### Step 2 — Apply to the Adidas sales data (IQR method)

```python
df = pd.read_excel('Adidas US Sales Datasets.xlsx')
df['total'] = df['Price per Unit'] * df['Units Sold']
```

Compute Q1, Q3 and IQR for the `total` column:

```python
q1, q3 = np.percentile(df['total'], [25, 75])
# q1 = 4065.25, q3 = 15864.5

iqr = q3 - q1
# iqr = 11799.25

lv = q1 - 1.5 * iqr  # -13633.625
uv = q3 + 1.5 * iqr  # 33563.375
```
{% endstep %}

{% step %}
### Step 3 — Filter data using IQR bounds

```python
odf = df.loc[df['total'].between(lv, uv)]
odf.shape  # 8849 rows × 10 columns

odf['total'].mean()
# np.float64(9446.502429653068)
```

The IQR filter removed extreme totals above the upper bound and reduced the mean from \~12455 to \~9446.
{% endstep %}
{% endstepper %}

Note: The IQR method is not guaranteed to detect outliers in every dataset — it depends on the distribution.

***

### Summary of methods shown

* Standard deviation method (e.g., ±3 STD).
* IQR (boxplot) method (Q1/Q3 ± 1.5 \* IQR).
* Percentiles/quartiles for exploratory understanding.

Choose the method based on your data characteristics and the goals of your analysis (robustness, presence of skew, etc.).

If you want, I can:

* Provide the exact code to save the cleaned dataset,
* Show how many rows/which rows were removed,
* Or produce visualizations (histogram/boxplot) before and after outlier removal. Which would you like next?
