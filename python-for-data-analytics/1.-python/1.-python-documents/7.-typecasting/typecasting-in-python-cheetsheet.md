---
description: >-
  Typecasting is converting a value from one data type to another in Python.
  This is useful when you need to perform operations on different data types.
---

# TypeCasting in Python CheetSheet

## Why Typecasting is Needed : <a href="#why-typecasting-is-needed" id="why-typecasting-is-needed"></a>

1. To perform calculations on strings that contain numbers
2. To convert data received from user input
3. To ensure compatibility between different data types
4. input() will always return data of string datatype

#### String To Integer

```
num_str = "10"
print(type(num_str))   # <class 'str'>
num_int = int(num_str) # "10" -> 10
print(type(num_int))   # <class 'int'>
```

```
<class 'str'>
<class 'int'>
```

#### String To Float

```
float_str = "3.14"
print(type(float_str))       # <class 'str'>
num_float = float(float_str) # "3.14" -> 3,.14
print(type(num_float))       # <class 'float'>
```

```
<class 'str'>
<class 'float'>
```

#### Converting a string containing a float value into an integer: Not Possible

```
num_str="3.14"
int_num = int(num_str)
print(int_num)   # Error -> converting a string containing float value into integer is not possible
```

#### Converting a String containing an integer into a float

```
num_str="3"
int_num = float(num_str)
print(int_num) # Output : 3.0
```

#### Converting a string value into an integer

```
string_var = "ConsoleFlare"
int_var = int(string_var)
print(int_var) # Error
```

#### Converting a string containing alphabets and numbers into Integers --> Not Possible

```
string_var="abcd12345"
int_var= int(string_var)
print(int_var)  # Error : Not Possible
```

```
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Cell In[1], line 3
      1 # Converting a String containing alphabets and numbers into Integer -> Not Possible
      2 string_var="abcd12345"
----> 3 int_var= int(string_var)
      4 print(int_var)  # Error : Not Possible

ValueError: invalid literal for int() with base 10: 'abcd12345'
```

#### Integer to Float

```
num = 7
num_float = float(num) # 7 -> 7.0
print(num_float)  # Output: 7.0
```

#### Integer to String

```
num = 100
num_str = str(num) # 100 -> "100"
print("Number is " + num_str)  # Output: Number is 100
```

#### Float to Integer

```
num = 3.99
num_int = int(num)  # 3.99 -> 3
print(num_int)  # Output: 3

# Note: Float to integer is not like rounding off... In integer typecasting the point values get simply ignored
```

#### Float to String

```
float_num = 3.14
float_str=str(float_num)
print(float_str,type(float_str))  # Output : 3.14 <class 'str'>
```

```
3.14 <class 'str'>
```

#### Integer to Boolean

```
print(bool(0))   # Output: False
print(bool(5))   # Output: True
```

#### Float to Boolean

```
print(bool(0.0))   # Output: False
print(bool(5.5))   # Output: True
```

#### String to Boolean

```
print(bool(""))      # Output: False
print(bool("Hello")) # Output: True
print(bool("S"))     # Output: True
print(bool(" "))     # Output : True
```

```
False
True
True
True
```

#### Boolean to Integer

```
print(int(True))  # Output : 1
print(int(False)) # Output : 0
```

```
1
0
```

#### Boolean to Float

```
print(float(True))  # Output : 1.0
print(float(False))  # Output : 0.0
```

```
1.0
0.0
```

#### Boolean to String

```
print(str(True))  # Output : True (string datatype)
print(str(False))  # Output : False (string datatype)
```

```
True
False
```

#### User Input

```
age = int(input("Enter your age: "))
height = float(input("Enter your height in meters: "))
print("Next year you will be", age + 1)
print("If you grow, your height will be", height + 0.1)
```
