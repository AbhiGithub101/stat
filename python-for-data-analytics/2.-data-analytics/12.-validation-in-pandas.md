# validation in pandas

Validation in pandas is used to check if we are following the rules. Having a wrong phone number or wrong Aadhaar card are some examples. We need to detect such invalid values and remove them to keep only correct data.

```python
# In [64]
import pandas as pd
```

## 1. Wrong Phone Number

```python
# In [65]
df = pd.read_csv('wrong phone number.csv')
df
```

|    | CustomerID | Phone       |
| -: | ---------: | ----------- |
|  0 |        101 | 9876543210  |
|  1 |        102 | 12345       |
|  2 |        103 | 9988776655  |
|  3 |        104 | abcdefghij  |
|  4 |        105 | 987654321   |
|  5 |        106 | 9876543210  |
|  6 |        107 | 98765432101 |
|  7 |        108 | 9123456789  |
|  8 |        109 | 98765abcde  |
|  9 |        110 | 9988776655  |

Rules for phone numbers:

{% stepper %}
{% step %}
### Rule

Phone number should have only 10 digits.
{% endstep %}

{% step %}
### Rule

It should contain only numeric characters (no letters or other symbols).
{% endstep %}
{% endstepper %}

```python
# In [66]
df['length'] = df['Phone'].str.len()
df
```

|    | CustomerID | Phone       | length |
| -: | ---------: | ----------- | -----: |
|  0 |        101 | 9876543210  |     10 |
|  1 |        102 | 12345       |      5 |
|  2 |        103 | 9988776655  |     10 |
|  3 |        104 | abcdefghij  |     10 |
|  4 |        105 | 987654321   |      9 |
|  5 |        106 | 9876543210  |     10 |
|  6 |        107 | 98765432101 |     11 |
|  7 |        108 | 9123456789  |     10 |
|  8 |        109 | 98765abcde  |     10 |
|  9 |        110 | 9988776655  |     10 |

```python
# In [67]
df['numbers'] = df['Phone'].str.isnumeric()
df
```

|    | CustomerID | Phone       | length | numbers |
| -: | ---------: | ----------- | -----: | ------- |
|  0 |        101 | 9876543210  |     10 | True    |
|  1 |        102 | 12345       |      5 | True    |
|  2 |        103 | 9988776655  |     10 | True    |
|  3 |        104 | abcdefghij  |     10 | False   |
|  4 |        105 | 987654321   |      9 | True    |
|  5 |        106 | 9876543210  |     10 | True    |
|  6 |        107 | 98765432101 |     11 | True    |
|  7 |        108 | 9123456789  |     10 | True    |
|  8 |        109 | 98765abcde  |     10 | False   |
|  9 |        110 | 9988776655  |     10 | True    |

### Filter out the right Phone Numbers

```python
# In [68]
df = df.loc[(df['length'] == 10) & (df['numbers'] == True)]
df
```

|    | CustomerID | Phone      | length | numbers |
| -: | ---------: | ---------- | -----: | ------- |
|  0 |        101 | 9876543210 |     10 | True    |
|  2 |        103 | 9988776655 |     10 | True    |
|  5 |        106 | 9876543210 |     10 | True    |
|  7 |        108 | 9123456789 |     10 | True    |
|  9 |        110 | 9988776655 |     10 | True    |

You can drop the helper columns:

```python
# In [69]
df = df.drop(columns=['length','numbers'])
df
```

|    | CustomerID | Phone      |
| -: | ---------: | ---------- |
|  0 |        101 | 9876543210 |
|  2 |        103 | 9988776655 |
|  5 |        106 | 9876543210 |
|  7 |        108 | 9123456789 |
|  9 |        110 | 9988776655 |

## 2. Wrong PAN Cards

PAN Format:

{% stepper %}
{% step %}
### Total length

10 characters
{% endstep %}

{% step %}
### First 5

First 5: letters (A-Z)
{% endstep %}

{% step %}
### Next 4

Next 4: digits (0-9)
{% endstep %}

{% step %}
### Last 1

Last 1: letter (A-Z)
{% endstep %}
{% endstepper %}

```python
# In [70]
df = pd.read_csv('wrong pan cards.csv')
df
```

|    | CustomerID | PAN        |
| -: | ---------: | ---------- |
|  0 |        101 | ABCDE1234F |
|  1 |        102 | AB1234CDE5 |
|  2 |        103 | KLMNO9012P |
|  3 |        104 | ABCDE12345 |
|  4 |        105 | UVWXY7890R |
|  5 |        106 | ABCDE12F4G |
|  6 |        107 | ZABCD2345S |
|  7 |        108 | 1234ABCDE5 |
|  8 |        109 | OPQRS4567V |
|  9 |        110 | ABCDE12345 |
| 10 |        111 | STUVW8901W |
| 11 |        112 | ABCDE12G4F |
| 12 |        113 | XYABC2345X |

```python
# In [71]
df['characters'] = df['PAN'].str.len()
df['First 5 Letter'] = df['PAN'].str[0:5]
df['Next 4 digit'] = df['PAN'].str[5:9]
df['Last 1 Letter'] = df['PAN'].str[-1]
df
```

|    | CustomerID | PAN        | characters | First 5 Letter | Next 4 digit | Last 1 Letter |
| -: | ---------: | ---------- | ---------: | -------------- | ------------ | ------------- |
|  0 |        101 | ABCDE1234F |         10 | ABCDE          | 1234         | F             |
|  1 |        102 | AB1234CDE5 |         10 | AB123          | 4CDE         | 5             |
|  2 |        103 | KLMNO9012P |         10 | KLMNO          | 9012         | P             |
|  3 |        104 | ABCDE12345 |         10 | ABCDE          | 1234         | 5             |
|  4 |        105 | UVWXY7890R |         10 | UVWXY          | 7890         | R             |
|  5 |        106 | ABCDE12F4G |         10 | ABCDE          | 12F4         | G             |
|  6 |        107 | ZABCD2345S |         10 | ZABCD          | 2345         | S             |
|  7 |        108 | 1234ABCDE5 |         10 | 1234A          | BCDE         | 5             |
|  8 |        109 | OPQRS4567V |         10 | OPQRS          | 4567         | V             |
|  9 |        110 | ABCDE12345 |         10 | ABCDE          | 1234         | 5             |
| 10 |        111 | STUVW8901W |         10 | STUVW          | 8901         | W             |
| 11 |        112 | ABCDE12G4F |         10 | ABCDE          | 12G4         | F             |
| 12 |        113 | XYABC2345X |         10 | XYABC          | 2345         | X             |

### Filter out right PAN Cards

```python
# In [72]
df = df.loc[
    (df['characters'] == 10) &
    (df['First 5 Letter'].str.isalpha()) &
    (df['Next 4 digit'].str.isnumeric()) &
    (df['Last 1 Letter'].str.isalpha())
]
df
```

|    | CustomerID | PAN        | characters | First 5 Letter | Next 4 digit | Last 1 Letter |
| -: | ---------: | ---------- | ---------: | -------------- | ------------ | ------------- |
|  0 |        101 | ABCDE1234F |         10 | ABCDE          | 1234         | F             |
|  2 |        103 | KLMNO9012P |         10 | KLMNO          | 9012         | P             |
|  4 |        105 | UVWXY7890R |         10 | UVWXY          | 7890         | R             |
|  6 |        107 | ZABCD2345S |         10 | ZABCD          | 2345         | S             |
|  8 |        109 | OPQRS4567V |         10 | OPQRS          | 4567         | V             |
| 10 |        111 | STUVW8901W |         10 | STUVW          | 8901         | W             |
| 12 |        113 | XYABC2345X |         10 | XYABC          | 2345         | X             |

```python
# In [73]
df = df.drop(columns=['characters','First 5 Letter','Next 4 digit','Last 1 Letter'])
df
```

|    | CustomerID | PAN        |
| -: | ---------: | ---------- |
|  0 |        101 | ABCDE1234F |
|  2 |        103 | KLMNO9012P |
|  4 |        105 | UVWXY7890R |
|  6 |        107 | ZABCD2345S |
|  8 |        109 | OPQRS4567V |
| 10 |        111 | STUVW8901W |
| 12 |        113 | XYABC2345X |

## How to use regex to do string manipulation

Regex stands for Regular Expression. It’s a pattern-matching tool that helps you find, check, or extract text based on a pattern.

Examples:

* Find digits: \d → matches any number (0-9)
* Find letters: \[a-zA-Z] → matches any uppercase or lowercase letter
* Check email format: \w+@\w+.\w+ → matches something like abc@gmail.com
* Start of a line: ^Hello → matches lines starting with “Hello”
* End of a line: world$ → matches lines ending with “world”

If you have a text "My number is 1234" and you use \d+, it will find "1234". Regex describes patterns in text to search, extract, or validate them.

### Wrong Phone Numbers (using regex)

```python
# In [74]
df = pd.read_csv('wrong phone number.csv')
df
```

```python
# In [75]
df = df.loc[df['Phone'].str.match(r'^\d{10}$')]
df
```

|    | CustomerID | Phone      |
| -: | ---------: | ---------- |
|  0 |        101 | 9876543210 |
|  2 |        103 | 9988776655 |
|  5 |        106 | 9876543210 |
|  7 |        108 | 9123456789 |
|  9 |        110 | 9988776655 |

### Wrong PAN Cards (using regex)

```python
# In [76]
df = pd.read_csv('wrong pan cards.csv')
df
```

```python
# In [77]
df = df.loc[df['PAN'].str.match('^[A-Z]{5}[0-9]{4}[A-Z]$')]
df
```

|    | CustomerID | PAN        |
| -: | ---------: | ---------- |
|  0 |        101 | ABCDE1234F |
|  2 |        103 | KLMNO9012P |
|  4 |        105 | UVWXY7890R |
|  6 |        107 | ZABCD2345S |
|  8 |        109 | OPQRS4567V |
| 10 |        111 | STUVW8901W |
| 12 |        113 | XYABC2345X |
