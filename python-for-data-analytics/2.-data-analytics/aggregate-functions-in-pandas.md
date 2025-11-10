# Aggregate Functions in Pandas

In Pandas, an aggregate function (or aggregation function) is a function that performs a calculation on a group of values and returns a single result — like sum, mean, min, max, count, etc.

```python
In [1]:
importpandasaspd
```

```python
In [3]:
df = pd.read_csv('employees.csv') df.head()
```

Out\[3]:

|    | Employee | Department | Age | Experience (Years) | Projects Completed | Training Hours | Client Rating | Bonus | Incentive | Salary |
| -: | -------- | ---------- | --: | -----------------: | -----------------: | -------------: | ------------: | ----: | --------: | -----: |
|  0 | Asha     | IT         |  28 |                  3 |                  5 |             40 |           4.5 |  5000 |      7000 |  60000 |
|  1 | Ravi     | IT         |  35 |                  7 |                  8 |             35 |           4.2 |  8000 |      9000 |  80000 |
|  2 | Neha     | HR         |  30 |                  4 |                  6 |             38 |           4.8 |  4000 |      6000 |  55000 |
|  3 | Arjun    | HR         |  42 |                 12 |                 10 |             25 |           4.1 |  9000 |      9500 |  90000 |
|  4 | Kiran    | Finance    |  38 |                  9 |                  9 |             30 |           4.6 |  7000 |      8000 |  75000 |

## sum()
