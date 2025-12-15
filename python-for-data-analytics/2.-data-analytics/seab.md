# seab

## Seaborn [¶](seab.md#Seaborn)

Seaborn is an advanced data visualization tool and it is used for advanced visualization. We are going to Cover these Plots :

1. relplot(relational plot) - `scatter line`
2. heatmap
3. regression - lmplot
4. catplot(categorical plot) - `strip swarm box violin boxen point bar count`
5. displot - `histplot kdeplot`

### Install Seaborn - [¶](seab.md#Install-Seaborn--)

`pip install seaborn`

### Import Libraries [¶](seab.md#Import-Libraries)

In \[1]:

importpandasaspd importmatplotlib.pyplotasplt importseabornassns

### 1. relplot [¶](seab.md#1.--relplot)

relplot is a high-level plotting function in Seaborn used to visualize relationships between numerical variables.

It shows how one numeric variable changes with another numeric variable.

relplot offers two plots.

1. scatter plot (default)
2. line plot

In \[4]:

df = pd.read\_csv('relplot data.csv') df.head()

Out\[4]:

|   | Order\_ID | Year | Month | City  | Customer\_Type | Order\_Value\_K | Delivery\_Time\_Min | Customer\_Rating | Distance\_KM | Day\_Type | Weather | Festival\_Period | Time\_Slot |
| - | --------- | ---- | ----- | ----- | -------------- | --------------- | ------------------- | ---------------- | ------------ | --------- | ------- | ---------------- | ---------- |
| 0 | 1001      | 2023 | Jan   | Delhi | Premium        | 1.2             | 18                  | 4.8              | 3            | Weekday   | Clear   | No               | Lunch      |
| 1 | 1002      | 2023 | Jan   | Delhi | Regular        | 0.5             | 25                  | 4.0              | 5            | Weekday   | Clear   | No               | Dinner     |
| 2 | 1003      | 2023 | Jan   | Delhi | Premium        | 1.5             | 22                  | 4.5              | 4            | Weekend   | Rainy   | Yes              | Dinner     |
| 3 | 1004      | 2023 | Jan   | Pune  | Regular        | 0.4             | 28                  | 3.8              | 6            | Weekday   | Rainy   | No               | Lunch      |
| 4 | 1005      | 2023 | Jan   | Pune  | Premium        | 1.0             | 20                  | 4.6              | 4            | Weekend   | Clear   | Yes              | Dinner     |

**Finding Relationship Between Delivery Time and Customer Rating**

In \[3]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image>)

Delivery time and Customer rating has negative relationship

**Segmentation - hue**

It uses different colors to separate categories in the data.

In \[6]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating', hue='Customer\_Type') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (1)>)

Regular Customers often get late deliveries rather than premium customer , which is the reason , regular customers give very less rating rather than premium customers.

**hue - palette**

In \[7]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating', hue='Customer\_Type', palette = { 'Premium':'Green' , 'Regular':'red' }) plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (2)>)

In \[10]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating', hue='Customer\_Type', palette = 'Reds') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (3)>)

### size [¶](seab.md#size)

It uses different sizes to separate categories in the data.

In \[12]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating', hue='Customer\_Type', palette = { 'Premium':'Green' , 'Regular':'red' }, size='Customer\_Rating') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (4)>)

**size - sizes**

In \[13]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating', hue='Customer\_Type', palette = { 'Premium':'Green' , 'Regular':'red' }, size='Customer\_Rating', sizes=(50,100)) plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (5)>)

### Segmentation - style [¶](seab.md#Segmentation---style)

It uses different sizes to separate categories in the data.

In \[20]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating', hue='Customer\_Type', palette = { 'Premium':'Green' , 'Regular':'red' }, size='Customer\_Rating', sizes=(50,100), style='Customer\_Type') # plt.legend( # bbox\_to\_anchor=(1, 1), # move legend outside # loc='upper left' # ) plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (6)>)

### Segmentation - row [¶](seab.md#Segmentation---row)

It uses different rows to separate categories in the data.

In \[23]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating', hue='Customer\_Type', palette = { 'Premium':'Green' , 'Regular':'red' }, size='Customer\_Rating', sizes=(50,100), style='Customer\_Type', row='Time\_Slot') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (7)>)

### Segmentation - col [¶](seab.md#Segmentation---col)

It uses different cols to separate categories in the data.

In \[24]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating', hue='Customer\_Type', palette = { 'Premium':'Green' , 'Regular':'red' }, size='Customer\_Rating', sizes=(50,100), style='Customer\_Type', col='Day\_Type') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (8)>)

In \[25]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating', hue='Customer\_Type', palette = { 'Premium':'Green' , 'Regular':'red' }, size='Customer\_Rating', sizes=(50,100), style='Customer\_Type', col='Day\_Type', row='Time\_Slot') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (9)>)

### 2. relplot - line [¶](seab.md#2.-relplot---line)

line plot is used to find pattern over time.

by default line plot uses average to show the line.

In \[27]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating', kind='line') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (10)>)

In \[29]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating', kind='line', estimator='sum') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (11)>)

#### An Example : [¶](seab.md#An-Example--:)

In \[31]:

df = pd.read\_excel('Adidas US Sales Datasets.xlsx') df\['total'] = df\['Price per Unit'] \* df\['Units Sold'] df

Out\[31]:

|      | Retailer    | Invoice Date | Region    | State         | City       | Product                   | Price per Unit | Units Sold | Sales Method | total   |
| ---- | ----------- | ------------ | --------- | ------------- | ---------- | ------------------------- | -------------- | ---------- | ------------ | ------- |
| 0    | Foot Locker | 2020-01-01   | Northeast | New York      | New York   | Men's Street Footwear     | 50.0           | 1200       | In-store     | 60000.0 |
| 1    | Foot Locker | 2020-01-02   | Northeast | New York      | New York   | Men's Athletic Footwear   | 50.0           | 1000       | In-store     | 50000.0 |
| 2    | Foot Locker | 2020-01-03   | Northeast | New York      | New York   | Women's Street Footwear   | 40.0           | 1000       | In-store     | 40000.0 |
| 3    | Foot Locker | 2020-01-04   | Northeast | New York      | New York   | Women's Athletic Footwear | 45.0           | 850        | In-store     | 38250.0 |
| 4    | Foot Locker | 2020-01-05   | Northeast | New York      | New York   | Men's Apparel             | 60.0           | 900        | In-store     | 54000.0 |
| ...  | ...         | ...          | ...       | ...           | ...        | ...                       | ...            | ...        | ...          | ...     |
| 9643 | Foot Locker | 2021-01-24   | Northeast | New Hampshire | Manchester | Men's Apparel             | 50.0           | 64         | Outlet       | 3200.0  |
| 9644 | Foot Locker | 2021-01-24   | Northeast | New Hampshire | Manchester | Women's Apparel           | 41.0           | 105        | Outlet       | 4305.0  |
| 9645 | Foot Locker | 2021-02-22   | Northeast | New Hampshire | Manchester | Men's Street Footwear     | 41.0           | 184        | Outlet       | 7544.0  |
| 9646 | Foot Locker | 2021-02-22   | Northeast | New Hampshire | Manchester | Men's Athletic Footwear   | 42.0           | 70         | Outlet       | 2940.0  |
| 9647 | Foot Locker | 2021-02-22   | Northeast | New Hampshire | Manchester | Women's Street Footwear   | 29.0           | 83         | Outlet       | 2407.0  |

9648 rows × 10 columns

In \[32]:

sns.relplot(data=df, x='Units Sold', y='total') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (12)>)

In \[34]:

sns.relplot(data=df, x='Units Sold', y='total', kind='line', marker='o') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (13)>)

In \[35]:

sns.relplot(data=df, x='Units Sold', y='total', kind='line', marker='o', estimator='sum') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (14)>)

In \[36]:

df = pd.read\_csv('relplot data.csv') df.head()

Out\[36]:

|   | Order\_ID | Year | Month | City  | Customer\_Type | Order\_Value\_K | Delivery\_Time\_Min | Customer\_Rating | Distance\_KM | Day\_Type | Weather | Festival\_Period | Time\_Slot |
| - | --------- | ---- | ----- | ----- | -------------- | --------------- | ------------------- | ---------------- | ------------ | --------- | ------- | ---------------- | ---------- |
| 0 | 1001      | 2023 | Jan   | Delhi | Premium        | 1.2             | 18                  | 4.8              | 3            | Weekday   | Clear   | No               | Lunch      |
| 1 | 1002      | 2023 | Jan   | Delhi | Regular        | 0.5             | 25                  | 4.0              | 5            | Weekday   | Clear   | No               | Dinner     |
| 2 | 1003      | 2023 | Jan   | Delhi | Premium        | 1.5             | 22                  | 4.5              | 4            | Weekend   | Rainy   | Yes              | Dinner     |
| 3 | 1004      | 2023 | Jan   | Pune  | Regular        | 0.4             | 28                  | 3.8              | 6            | Weekday   | Rainy   | No               | Lunch      |
| 4 | 1005      | 2023 | Jan   | Pune  | Premium        | 1.0             | 20                  | 4.6              | 4            | Weekend   | Clear   | Yes              | Dinner     |

In \[38]:

sns.relplot(data=df, x='Delivery\_Time\_Min', y='Customer\_Rating', kind='line', hue='Customer\_Type') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (15)>)

#### Let's Explore With Examples [¶](seab.md#Let's-Explore-With-Examples)

In \[42]:

df = pd.read\_excel('Adidas US Sales Datasets.xlsx') df\['total'] = df\['Price per Unit'] \* df\['Units Sold'] df\['Invoice Date'] = pd.to\_datetime(df\['Invoice Date'],format='%Y-%m-%d') df\['Year'] = df\['Invoice Date'].dt.year df.head()

Out\[42]:

|   | Retailer    | Invoice Date | Region    | State    | City     | Product                   | Price per Unit | Units Sold | Sales Method | total   | Year |
| - | ----------- | ------------ | --------- | -------- | -------- | ------------------------- | -------------- | ---------- | ------------ | ------- | ---- |
| 0 | Foot Locker | 2020-01-01   | Northeast | New York | New York | Men's Street Footwear     | 50.0           | 1200       | In-store     | 60000.0 | 2020 |
| 1 | Foot Locker | 2020-01-02   | Northeast | New York | New York | Men's Athletic Footwear   | 50.0           | 1000       | In-store     | 50000.0 | 2020 |
| 2 | Foot Locker | 2020-01-03   | Northeast | New York | New York | Women's Street Footwear   | 40.0           | 1000       | In-store     | 40000.0 | 2020 |
| 3 | Foot Locker | 2020-01-04   | Northeast | New York | New York | Women's Athletic Footwear | 45.0           | 850        | In-store     | 38250.0 | 2020 |
| 4 | Foot Locker | 2020-01-05   | Northeast | New York | New York | Men's Apparel             | 60.0           | 900        | In-store     | 54000.0 | 2020 |

In \[45]:

sns.relplot(data=df, x='Units Sold', y='total', ) plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (12)>)

**Region Wise**

In \[46]:

sns.relplot(data=df, x='Units Sold', y='total', hue='Region') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (16)>)

In \[52]:

sns.relplot(data=df, x='Units Sold', y='total', col='Region', col\_wrap=2, hue='Region') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (17)>)

#### Yearly Average Sales [¶](seab.md#Yearly-Average-Sales)

In \[50]:

sns.relplot(data=df, x='Year', y='total', kind='line') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (18)>)

In \[51]:

sns.relplot(data=df, x='Year', y='total', kind='line', hue='Region') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (19)>)

#### Total Sales [¶](seab.md#Total-Sales)

In \[53]:

sns.relplot(data=df, x='Year', y='total', kind='line', hue='Region', estimator='sum') plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (20)>)

## 📊 Correlation Heatmap — Notebook Explanation [¶](seab.md#%F0%9F%93%8A-Correlation-Heatmap-%E2%80%94-Notebook-Explanation)

### 📌 What is Correlation? [¶](seab.md#%F0%9F%93%8C-What-is-Correlation?)

Correlation measures **how strongly two numerical variables are related**.

* Value range: **-1 to +1**
* `+1` → strong positive relationship
* `-1` → strong negative relationship
* `0` → no relationship

***

### 📌 What is a Correlation Heatmap? [¶](seab.md#%F0%9F%93%8C-What-is-a-Correlation-Heatmap?)

A **correlation heatmap** is a visual way to represent correlation values using **colors**.

Instead of reading numbers, we **interpret color intensity**.

***

### 🎨 How to Read Colors in a Correlation Heatmap [¶](seab.md#%F0%9F%8E%A8-How-to-Read-Colors-in-a-Correlation-Heatmap)

| Color Meaning         | Interpretation              |
| --------------------- | --------------------------- |
| Dark positive color   | Strong positive correlation |
| Dark negative color   | Strong negative correlation |
| Light / neutral color | Weak or no correlation      |

👉 **Darker the color = stronger the relationship**

***

### 📌 Why Use a Correlation Heatmap? [¶](seab.md#%F0%9F%93%8C-Why-Use-a-Correlation-Heatmap?)

* To quickly **identify relationships**
* To detect **multicollinearity**
* To find **important features** in data analysis

***

### 📌 Example Interpretation [¶](seab.md#%F0%9F%93%8C-Example-Interpretation)

If a heatmap shows:

* `Hours_Studied` vs `Marks` → dark positive color → More study hours leads to higher marks
* `Speed` vs `Travel_Time` → dark negative color → Higher speed reduces travel time

***

### 🧠 Key Takeaway [¶](seab.md#%F0%9F%A7%A0-Key-Takeaway)

> A correlation heatmap visually shows how strongly and in which direction numerical variables are related using color intensity.

***

In \[54]:

df = pd.read\_csv('Sleep\_health\_and\_lifestyle\_dataset.csv') df

Out\[54]:

|     | Person ID | Gender | Age | Occupation           | Sleep Duration | Quality of Sleep | Physical Activity Level | Stress Level | BMI Category | Blood Pressure | Heart Rate | Daily Steps | Sleep Disorder |
| --- | --------- | ------ | --- | -------------------- | -------------- | ---------------- | ----------------------- | ------------ | ------------ | -------------- | ---------- | ----------- | -------------- |
| 0   | 1         | Male   | 27  | Software Engineer    | 6.1            | 6                | 42                      | 6            | Overweight   | 126/83         | 77         | 4200        | NaN            |
| 1   | 2         | Male   | 28  | Doctor               | 6.2            | 6                | 60                      | 8            | Normal       | 125/80         | 75         | 10000       | NaN            |
| 2   | 3         | Male   | 28  | Doctor               | 6.2            | 6                | 60                      | 8            | Normal       | 125/80         | 75         | 10000       | NaN            |
| 3   | 4         | Male   | 28  | Sales Representative | 5.9            | 4                | 30                      | 8            | Obese        | 140/90         | 85         | 3000        | Sleep Apnea    |
| 4   | 5         | Male   | 28  | Sales Representative | 5.9            | 4                | 30                      | 8            | Obese        | 140/90         | 85         | 3000        | Sleep Apnea    |
| ... | ...       | ...    | ... | ...                  | ...            | ...              | ...                     | ...          | ...          | ...            | ...        | ...         | ...            |
| 369 | 370       | Female | 59  | Nurse                | 8.1            | 9                | 75                      | 3            | Overweight   | 140/95         | 68         | 7000        | Sleep Apnea    |
| 370 | 371       | Female | 59  | Nurse                | 8.0            | 9                | 75                      | 3            | Overweight   | 140/95         | 68         | 7000        | Sleep Apnea    |
| 371 | 372       | Female | 59  | Nurse                | 8.1            | 9                | 75                      | 3            | Overweight   | 140/95         | 68         | 7000        | Sleep Apnea    |
| 372 | 373       | Female | 59  | Nurse                | 8.1            | 9                | 75                      | 3            | Overweight   | 140/95         | 68         | 7000        | Sleep Apnea    |
| 373 | 374       | Female | 59  | Nurse                | 8.1            | 9                | 75                      | 3            | Overweight   | 140/95         | 68         | 7000        | Sleep Apnea    |

374 rows × 13 columns

In \[60]:

cdf = df\[ \['Sleep Duration','Quality of Sleep','Stress Level','Age'] ].corr() cdf

Out\[60]:

|                  | Sleep Duration | Quality of Sleep | Stress Level | Age       |
| ---------------- | -------------- | ---------------- | ------------ | --------- |
| Sleep Duration   | 1.000000       | 0.883213         | -0.811023    | 0.344709  |
| Quality of Sleep | 0.883213       | 1.000000         | -0.898752    | 0.473734  |
| Stress Level     | -0.811023      | -0.898752        | 1.000000     | -0.422344 |
| Age              | 0.344709       | 0.473734         | -0.422344    | 1.000000  |

In \[61]:

sns.heatmap(data=cdf,annot=True) plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (21)>)

### regression - lmplot [¶](seab.md#regression---lmplot)

In \[62]:

df = pd.read\_excel('Adidas US Sales Datasets.xlsx') df\['total'] = df\['Price per Unit'] \* df\['Units Sold'] df.head()

Out\[62]:

|   | Retailer    | Invoice Date | Region    | State    | City     | Product                   | Price per Unit | Units Sold | Sales Method | total   |
| - | ----------- | ------------ | --------- | -------- | -------- | ------------------------- | -------------- | ---------- | ------------ | ------- |
| 0 | Foot Locker | 2020-01-01   | Northeast | New York | New York | Men's Street Footwear     | 50.0           | 1200       | In-store     | 60000.0 |
| 1 | Foot Locker | 2020-01-02   | Northeast | New York | New York | Men's Athletic Footwear   | 50.0           | 1000       | In-store     | 50000.0 |
| 2 | Foot Locker | 2020-01-03   | Northeast | New York | New York | Women's Street Footwear   | 40.0           | 1000       | In-store     | 40000.0 |
| 3 | Foot Locker | 2020-01-04   | Northeast | New York | New York | Women's Athletic Footwear | 45.0           | 850        | In-store     | 38250.0 |
| 4 | Foot Locker | 2020-01-05   | Northeast | New York | New York | Men's Apparel             | 60.0           | 900        | In-store     | 54000.0 |

In \[69]:

sns.lmplot(data=df, x='Units Sold', y='total', scatter\_kws={'color': 'blue'}, line\_kws={'color': 'red'}, col='Region', col\_wrap=2 ) plt.show()

![No description has been provided for this image](<../../.gitbook/assets/Unknown image (22)>)

In \[ ]:
