# String Function In Pandas

If you are working on a dataset, there are scenarios where you need to perform string operations / manipulation.

## String Function In Pandas

To demonstrate, consider this sample dataframe:

```python
import pandas as pd
df = pd.read_csv('string dataset.csv')
df
```

Output (DataFrame):

|   | CustomerID | FirstName | LastName | Address                  | Feedback                               | PhoneNumber   |
| - | ---------- | --------- | -------- | ------------------------ | -------------------------------------- | ------------- |
| 0 | 101        | RaHul     | Sharma   | 221B baker street, delhi | Product was good but DELIVERY was late | 98765432      |
| 1 | 102        | Priya     | Singh    | mg road, bengaluru       | Packing was excellent!!                | 9988776655    |
| 2 | 103        | Anil      | Kapoor   | sector 22, noida         | Quality not same as shown              | 123456789012  |
| 3 | 104        | sneha     | Agarwal  | park street, kolkata     | Delay of 5 days. not satisfied         | 90807060      |
| 4 | 105        | Rohan     | Mehta    | andheri east, mumbai     | Product damaged. refund in 7 days?     | 9090909090    |
| 5 | 106        | Meera     | Verma    | baner road, pune         | Delivered early!! very happy           | 8008008008    |
| 6 | 107        | amit      | Kumar    | gomti nagar, lucknow     | Color was different from the website   | 9876543210987 |
| 7 | 108        | SwaTi     | Joshi    | anna salai, chennai      | Double payment deducted                | 88112         |
| 8 | 109        | Ravi      | Shukla   | ring road, ahmedabad     | Wrong item delivered                   | 9999999999    |
| 9 | 110        | Nidhi     | Gupta    | civil lines, jaipur      | Refund amount incorrect by 150 rupees  | 989898989     |

To use string functions on columns, use the `str` accessor. Just like `dt` brings datetime functions, `str` brings string functions.

### strip function

`strip` removes white spaces from the left and right side of the string.

Example:

```python
df['FirstName'] = df['FirstName'].str.strip()
df
```

Output (DataFrame):

|   | CustomerID | FirstName | LastName | Address                  | Feedback                               | PhoneNumber   |
| - | ---------- | --------- | -------- | ------------------------ | -------------------------------------- | ------------- |
| 0 | 101        | RaHul     | Sharma   | 221B baker street, delhi | Product was good but DELIVERY was late | 98765432      |
| 1 | 102        | Priya     | Singh    | mg road, bengaluru       | Packing was excellent!!                | 9988776655    |
| 2 | 103        | Anil      | Kapoor   | sector 22, noida         | Quality not same as shown              | 123456789012  |
| 3 | 104        | sneha     | Agarwal  | park street, kolkata     | Delay of 5 days. not satisfied         | 90807060      |
| 4 | 105        | Rohan     | Mehta    | andheri east, mumbai     | Product damaged. refund in 7 days?     | 9090909090    |
| 5 | 106        | Meera     | Verma    | baner road, pune         | Delivered early!! very happy           | 8008008008    |
| 6 | 107        | amit      | Kumar    | gomti nagar, lucknow     | Color was different from the website   | 9876543210987 |
| 7 | 108        | SwaTi     | Joshi    | anna salai, chennai      | Double payment deducted                | 88112         |
| 8 | 109        | Ravi      | Shukla   | ring road, ahmedabad     | Wrong item delivered                   | 9999999999    |
| 9 | 110        | Nidhi     | Gupta    | civil lines, jaipur      | Refund amount incorrect by 150 rupees  | 989898989     |

You can strip multiple columns:

```python
df['LastName'] = df['LastName'].str.strip()
df['Address'] = df['Address'].str.strip()
df['Feedback'] = df['Feedback'].str.strip()
df
```

Output (DataFrame) — same structure with trimmed whitespace.

### lower / upper / swapcase / title / capitalize

These methods change case or capitalization.

Example sequence:

```python
df['Address'] = df['Address'].str.title()
df['Address'] = df['Address'].str.capitalize()
df['Address'] = df['Address'].str.swapcase()
df['Address'] = df['Address'].str.lower()
df
```

Output (DataFrame): addresses shown in lower case.

### len function

Counts the number of characters in a value.

```python
df['count'] = df['FirstName'].str.len()
df
```

Output includes new column `count` with character lengths of FirstName.

For phone numbers, first cast to string, then measure length:

```python
df['PhoneNumber'] = df['PhoneNumber'].astype(str)
df['Phone Length'] = df['PhoneNumber'].str.len()
df
```

Output includes `Phone Length` column.

### replace

Used to replace substrings or characters.

```python
df['Address'] = df['Address'].str.replace('street','st.')
df
```

And removing punctuation from feedback:

```python
df['Feedback'] = df['Feedback'].str.replace('!','').str.replace('?','')
df
```

Output: punctuation removed in `Feedback`, `street` replaced by `st.` in `Address`.

### split(expand=True)

Split values by a delimiter.

```python
df['Address'].str.split(',')
```

This returns a Series of lists. To expand into separate columns:

```python
df['Address'].str.split(',', expand=True)
```

Output (expanded):

|   | 0              | 1         |
| - | -------------- | --------- |
| 0 | 221b baker st. | delhi     |
| 1 | mg road        | bengaluru |
| 2 | sector 22      | noida     |
| 3 | park st.       | kolkata   |
| 4 | andheri east   | mumbai    |
| 5 | baner road     | pune      |
| 6 | gomti nagar    | lucknow   |
| 7 | anna salai     | chennai   |
| 8 | ring road      | ahmedabad |
| 9 | civil lines    | jaipur    |

Assign to new columns:

```python
df['Area'] = df['Address'].str.split(',', expand=True)[0]
df['City'] = df['Address'].str.split(',', expand=True)[1]
df
```

Output includes `Area` and `City` columns.

### contains()

Returns True if string contains the keyword (supports regex). Useful with `loc` to filter rows.

Examples:

```python
df.loc[df['Feedback'].str.contains('Refund', case=False)]
```

Matches rows where Feedback contains "Refund" (case-insensitive).

Combine conditions:

```python
df.loc[df['Feedback'].str.contains("refund", case=False) | df['Feedback'].str.contains("not satisfied", case=False)]
```

Or use a regex alternation:

```python
df.loc[df['Feedback'].str.contains('Refund|not satisfied', case=False)]
```

To require multiple keywords (AND):

```python
df.loc[df['Feedback'].str.contains('damaged', case=False) & df['Feedback'].str.contains('Refund', case=False)]
```

Note: there's no shortcut operator inside a single `contains` call for logical AND — combine expressions with `&`.

### startswith()

Checks if a string starts with the given keyword. There's no `case` parameter for `startswith`, so standardize case first if needed.

```python
df['Address'] = df['Address'].str.lower()
df.loc[df['Address'].str.startswith('park')]
```

### endswith()

Checks if a string ends with the given keyword. Also has no `case` parameter; standardize case first.

```python
df['Address'] = df['Address'].str.lower()
df.loc[df['Address'].str.endswith('kolkata')]
```

### string concatenation

You can concatenate strings from columns:

```python
df['full name'] = df['FirstName'] + ' ' + df['LastName']
df
```

Output includes `full name` column.

### indexing

Access characters by position:

```python
df['area code'] = df['Address'].str[0]
df
```

Adds `area code` column with first character of `Address`.

### slicing

Slice substrings using Python slice notation:

```python
df['short name'] = df['FirstName'].str[0:3]
df
```

Adds `short name` column.

You can combine operations to create more complex codes:

```python
df['unique code'] = df['FirstName'].str[0:3] + '-' + df['CustomerID'].astype(str) + '-' + df['City'].str[::-1]
df
```

Output includes `unique code` column, e.g. `RaH-101-ihled`.

***

End of examples.
