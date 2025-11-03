# 1 Introduction To Numpy

## Introduction to Numpy

Numpy is a tool/library we use for data calculation.

### How to install numpy

You can go to your terminal and write:

```bash
pip install numpy
```

### Import Numpy

If you have installed it and you want to use it, you must import it.

```python
import numpy as np  # np is a short name that we give to numpy
```

### Let's take an example

```python
score = [20, 50, 30, 70, 10]
score
```

Output:

```
[20, 50, 30, 70, 10]
```

### divide each score with 100

```python
score / 100
```

Error:

```
TypeError: unsupported operand type(s) for /: 'list' and 'int'
```

Note: Mathematical operations are not possible on a Python list.

```python
score + 100
```

Error:

```
TypeError: can only concatenate list (not "int") to list
```

```python
score - 100
```

Error:

```
TypeError: unsupported operand type(s) for -: 'list' and 'int'
```

List is not made for mathematical operations. Lists are mainly made to store values.

### List to array Conversion

Because lists are not made for mathematical operations, if you want to do mathematical operations you need to convert the list into a Numpy array.

#### What is Array?

Array is Numpy's list. An array is like a list but it can perform mathematical operations.

#### How to convert list into array?

We have the `np.array` function in numpy to convert a list into an array.

```python
score = np.array(score)
score
```

Output:

```
array([20, 50, 30, 70, 10])
```

Now you can perform mathematical / element-wise operations:

```python
score / 100
```

Output:

```
array([0.2, 0.5, 0.3, 0.7, 0.1])
```

```python
score + 100
```

Output:

```
array([120, 150, 130, 170, 110])
```

```python
score - 100
```

Output:

```
array([-80, -50, -70, -30, -90])
```

Properties of Numpy Array:

1. A Python list can have multiple data types, for example: \[1, 2, 3, 'abhi']
2. A Numpy array has a single data type: \[1, 2, 3], \[1.0, 2.0, 3.0], or \['1', '2', '3']

### int and float

When you have a list of ints and floats, the final array is always float (to avoid data loss).

```python
score = [10, 20, 30, 65.78, 76.58]
score = np.array(score)
score
```

Output:

```
array([10.  , 20.  , 30.  , 65.78, 76.58])
```

### int and string

When you have a list of ints and strings, the final array will be of string dtype.

```python
score = [10, 20, 30, 'abhi']
score = np.array(score)
score
```

Output:

```
array(['10', '20', '30', 'abhi'], dtype='<U21')
```

```python
score = [10, 20, 30, '40']
score = np.array(score)
score
```

Output:

```
array(['10', '20', '30', '40'], dtype='<U21')
```

### float and string and int

```python
score = [10, 10, 5, '49']
score = np.array(score)
score
```

Output:

```
array(['10', '10', '5', '49'], dtype='<U21')
```

### you can forcibly change the data type of array values

You can forcibly change the data type of array values by using the `dtype` parameter.

```python
score = [10, 20, 30, 40.5, 60.7]
score = np.array(score, dtype=int)
score
```

Output:

```
array([10, 20, 30, 40, 60])
```

```python
score = [10, 20, 30, 40.5, 60.7]
score = np.array(score, dtype=str)
score
```

Output:

```
array(['10', '20', '30', '40.5', '60.7'], dtype='<U4')
```

```python
score = [10, 20, 30, '50']
score = np.array(score, dtype=int)
score
```

Output:

```
array([10, 20, 30, 50])
```

## limitation

```python
score = [10, 20, 'abhi']
score = np.array(score, dtype=int)
score
```

Error:

```
ValueError: invalid literal for int() with base 10: 'abhi'
```
