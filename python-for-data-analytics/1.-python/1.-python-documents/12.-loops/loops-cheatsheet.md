---
description: Complete Python Loops cheatsheet with clear examples for quick revision
---

# Loops Cheatsheet

## **WHAT IS A LOOP?**

A loop is used to **repeat a block of code multiple times** until a **condition** is met. Instead of writing the same code again and again, we use loops.

### Real-life examples:

* Asking attendance of 50 students one by one
* Printing numbers from 1 to 10

### Why do we need loops?

* To save time
* To reduce code repetition
* To work with lists, strings, and ranges
* To automate repetitive tasks

### Types of loops in Python

* while loop
* for loop

***

## while Loop

**Definition** \
A while loop is used when we do not know how many times the loop will run. It runs as long as a condition is true.

#### **Syntax**

```
while condition:
    code to repeat
```

{% stepper %}
{% step %}
### Example: Factorial using while loop

```python
result = 1
i = 1
while i <= 5:
    result = result * i
    i = i + 1

print(f'The factorial of 5 is:{result}')
# OUTPUT
# The factorial of 5 is: 120
```
{% endstep %}

{% step %}
### Example: Print numbers from 1 to 5

```python
i = 1
while i <= 5:
    print(i)
    i += 1
# Note -> i += 1 is very important, otherwise the loop will run forever (infinite loop)
```
{% endstep %}

{% step %}
### Example: Print each character of a string using while loop

```python
name = "Python"
i = 0
while i < len(name):
    print(name[i])
    i += 1
```
{% endstep %}

{% step %}
### Example: Print each word in a sentence using while loop

```python
sentence = "Python is fun"
words = sentence.split()
i = 0
while i < len(words):
    print(words[i])
    i += 1
# OUTPUT :
# Python
# is
# fun
```
{% endstep %}
{% endstepper %}

***

## for Loop

**Definition**\
A for loop is used when we know in advance how many times the loop should run.

Syntax

```
for variable in sequence:
    code to repeat
```

{% stepper %}
{% step %}
### Example: Print numbers from 1 to 5

```python
for i in range(1, 6):
    print(i)
# OUTPUT:
# 1
# 2
# 3
# 4
# 5
```

**Note: range(1, 6) means numbers from 1 to 5 (6 is excluded).**
{% endstep %}

{% step %}
### Example: Print each character of a string

```python
for ch in "Python":
    print(ch)
# OUTPUT:
# P
# y
# t
# h
# o
# n
```
{% endstep %}

{% step %}
### Example: Loop through a list

```python
fruits = ["apple", "banana", "mango"]
for each_fruit in fruits:
    print(each_fruit)
# OUTPUT:
# apple
# banana
# mango
```
{% endstep %}
{% endstepper %}

### Common use of range()

* range(5) → 0 to 4
* range(1, 5) → 1 to 4
* range(1, 10, 2) → 1, 3, 5, 7, 9

## Iterating using range()

**Definition**&#x20;

range() is used to generate a sequence of numbers. It is commonly used with for loops when we want to repeat something a fixed number of times.

Syntax

```
range(start, stop, step)
```

* start → starting number (default: 0)
* stop → ending number (not included)
* step → gap between numbers (default: 1)

Examples:

```python
# Print numbers from 0 to 4
for i in range(5):
    print(i)

# Print numbers from 1 to 10
for i in range(1, 11):
    print(i)

# Print even numbers
for i in range(2, 11, 2):
    print(i)
```

***

## Iterating using enumerate()

**Definition**&#x20;

enumerate() is used when we want both the index and the value while looping through a sequence  (list, string, etc.).

**Syntax**

```
enumerate(sequence, start=0)
```

Examples:

```python
# Loop through a list with index
fruits = ["apple", "banana", "mango"]
for index, fruit in enumerate(fruits):
    print(index, fruit)
# Output :
# 0 apple
# 1 banana
# 2 mango

# Start index from 1
for index, fruit in enumerate(fruits, start=1):
    print(index, fruit)
```

***

## Infinite Loop

If the condition never becomes false, the loop runs forever.

```py
# Example of infinite loop 
i = 1
while i <= 5:
    print(i)
# Note -> Always update the condition variable.
```

***

## Loop Control Statements

These statements control the flow of loops.

{% stepper %}
{% step %}
### break

**Definition :** \
break is used to stop the loop immediately.

```python
for i in range(1, 10):
    if i == 5:
        break
    print(i)
    
# OUTPUT:
# 1
# 2
# 3
# 4
```
{% endstep %}

{% step %}
### continue

**Definition :** \
continue is used to skip the current iteration and move to the next one.

```python
for i in range(1, 6):
    if i == 3:
        continue
    print(i)
# OUTPUT:
# 1
# 2
# 4
# 5
```
{% endstep %}

{% step %}
### pass

**Definition :** \
pass is used when we don’t want to write code yet, but need the loop syntax.

```python
for i in range(5):
    pass
# NOTE -> No output, no error.
```
{% endstep %}
{% endstepper %}

***

## Nested Loops (Loop inside Loop)

**Definition :** \
A loop inside another loop is called a nested loop.

{% stepper %}
{% step %}
### Example 1

```python
persons = [{'name': 'John', 'sex': 'Male'}, {'name': 'Jane', 'sex': 'Female'}]
for person in persons:
    for key in person:
        print(key, ":", person[key])
    print(" ")
    
# OUTPUT:
# name : John
# sex : Male
#
# name : Jane
# sex : Female
```
{% endstep %}

{% step %}
### Example 2

```python
days = ['Monday', 'Tuesday', 'Wednesday']
fruits = ['apple', 'banana', 'guava']
for day in days:
    for fruit in fruits:
        print(day, fruit)
        
# OUTPUT:
# Monday apple
# Monday banana
# Monday guava
# Tuesday apple
# Tuesday banana
# Tuesday guava
# Wednesday apple
# Wednesday banana
# Wednesday guava
```
{% endstep %}
{% endstepper %}
