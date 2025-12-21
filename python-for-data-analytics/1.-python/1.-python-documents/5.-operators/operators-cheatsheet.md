---
description: Complete Python operators cheatsheet with clear examples for quick revision
---

# Operators Cheatsheet

## Arithmetic Operators <a href="#arithmetic-operators" id="arithmetic-operators"></a>

#### 1.   Addition operators  ( + )  -----> Used to perform addition

```python
a=10
b=20
c=a+b # 10+20=30
print(c)
```

#### 2.   Subtraction Operators ( - ) -----> Used to perform subtraction

```python
x=25
y=15
z=x-y # 25-15=10
print(z)
```

#### 3.   Multiplication Operators ( \* ) -----> Used to perform multiplication

```python
a=5
b=20
c=a*b # 5*20=100
print(c)

# Note: * works differently for sequences like string, list, etc. , which will be discussed later.
```

#### 4.   Division Operators ( / )  -----> Always gives output in float data type

```python
x=30
y=10
z=x/y # 30/10=3.0
print(z)
```

#### 5.   Floor Division ( // ) -----> Always gives output in Integer data type

```python
a=15
b=4
c=a//b # 15//4=3
print(c)
```

#### 6.   Exponent (Raise to the power operator) ( \*\* ) -----> Left side value must be Base whereas Right side value must be Power

```python
x=2
y=3
z=x**y # 2**3=8 --> 2 is base whereas 3 is its power
print(z)
```

#### 7.   Modulus Operator ( % )  -----> It returns the Remainder after the division of two operands. It always gives output in Integer data type

```python
a=23
b=3
c=a%b # 23%3=2
print(c)
```

## Assignment Operators <a href="#assignment-operators" id="assignment-operators"></a>

#### 1.   Assignment Operator ( = ) -----> It assigns the value of the right expression to the Left operand

```python
a=30
print(a)
```

#### 2.   Addition Assignment Operators ( += )

```python
x=25
x+=5 # it works like: x=x+5 => x=25+5=30
print(x)
# Note: Just like += is working , similarly -= , *= , /= , //= ,**= also works
```

#### 3.   Subtraction Assignment Operators ( -= )

```python
a=45
a-=15 #30
print(a)
```

#### 4.   Multiplication Assignment operators ( \*= )

```python
x=6
x*=7 #42
print(x)
```

#### 5.   Division Assignment operators ( /= )

```python
a=45
a/=9# 5.0
print(a)
```

#### 6.   Floor Division operators ( /= )

```python
x=35
x//=5 # 7
print(x)
```

#### 7.   Exponentiation Assignment Operators ( \*\*= )

```python
a=4
a**=3 # 64
print(a)
```

## Comparison Operators <a href="#comparison-operators" id="comparison-operators"></a>

**Used to compare values and return True or False**

#### 1.   Greater Than ( > ) ------> Returns True if Left value if greater than Right value

```python
x=5
print(x>2)  # True
print(x>10) #False
```

```
True
False
```

#### 2.   Greater than or Equals to ( >= )  -----> Returns True if the Left value is greater than or Equal to the Right value

```python
x=5
print(x>=10) # False
print(x>=5)  # True
print(x>=4) # True
```

```
False
True
True
```

#### 3.   Smaller than ( < ) -----> Returns True if Left value is Less than Right value

```python
x=5
print(x<10) # True
print(x<5)  # False
```

```
True
False
```

#### 4.   Smaller than Equals to ( <= ) -----> Returns True if the Left value is Less than or Equal to the Right value

```python
x=5
print(x<=10) # True
print(x<=5)  # True
print(x<=2)  #False
```

```
True
True
False
```

#### 5.   Equals to ( == ) -----> Returns True if two values are equal

```python
x=5
print(x==5) #True
print(x==10) #False
print(x==-5) #False
```

```
True
False
False
```

#### 6.   Not Equals to ( != ) -----> Returns True if Two values are not equals

```python
x=5
print(x!=5)  #False
print(x!=10) #True
```

```
False
True
```

## Logical Operators <a href="#logical-operators" id="logical-operators"></a>

1. and operator
2. or operator
3. not operator

#### 1.   and Operators -----> Returns True if both conditions are True

```python
# a)
a = 10
b = 5
c = 15
print(a > b and b < c)  # True, because both conditions are True
print(a > c and b < a) # False, first condition is False

# b)
x = True
y = False
print(x and y)  # False
```

```
True
False
False
```

#### 2.   or Operators -----> Returns True if at least one condition is True

```python
# a)
a = 10
b = 5
c = 15
print(a > b or b > c)  # True, because first condition is True
print(a < b or b > c)  # False, both conditions are False

# b)
x = True
y = False
print(x or y)

# Used to combine multiple conditions and return True or False (and, or)
```

```
True
False
True
```

#### 3.   not Operators -----> It returns True if the condition is False, and returns False if the condition is True

```python
x=True
print(not x) #False
print(x) # True


# It only works with boolean expressions or values that can be interpreted as True or False.
```

```
True
False
```
