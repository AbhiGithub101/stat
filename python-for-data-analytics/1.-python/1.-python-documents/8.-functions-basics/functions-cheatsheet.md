---
description: Complete Python Functions cheatsheet with clear examples for quick revision
---

# Functions Cheatsheet

> Types of a Function:
>
> * <mark style="color:$info;">**Built-in Functions**</mark>: Functions predefined in Python. Example: `print()`, `type()`.
> * <mark style="color:$info;">**User-Defined Functions**</mark>: Functions that a user defines for a particular task.

> Two Important Aspects of a Function:
>
> * <mark style="color:$info;">**Defining a Function**</mark>: Define what specific task the function will do.
> * <mark style="color:$info;">**Calling a Function**</mark>: Invoke the function to perform the task. You cannot call a function before defining it.

{% stepper %}
{% step %}
### Syntax: Defining a function

```python
def function_name():  # function name
    print('hello')    # function body
```
{% endstep %}

{% step %}
### Basic Function (No Parameters, No Arguments)

```python
def greet():
    print("Hello, Welcome to Python")

greet()  # This calls the greet() function.
```
{% endstep %}

{% step %}
### Function with Default Parameters

We can pass default parameters while defining the function.

```python
def greet(name='Ayush'):
    print('Hello', name)

greet()
```
{% endstep %}

{% step %}
### Function with Parameters

```python
def greet(name):
    print("Hello", name)

greet("Shikher")  # Calls the greet() function with an argument.
```
{% endstep %}

{% step %}
### Function with Return Value

```python
def add(a, b):
    return a + b  # returns the sum of two numbers.

result = add(10, 20)  # returns 30
print(result)         # Output: 30
```
{% endstep %}

{% step %}
### Function with Parameters & Return

```python
def square(num):
    return num * num  # returns the square of the number.

print(square(5))  # Output: 25
```
{% endstep %}

{% step %}
### Function with Multiple Parameters

```python
def area_rectangle(length, breadth):
    return length * breadth  # returns the area of a rectangle.

print(area_rectangle(5, 4))  # Output: 20
```
{% endstep %}
{% endstepper %}

## Keyword Arguments

Definition: Keyword arguments (or kwargs) allow you to pass values to a function by explicitly naming the parameters. They make code more readable and flexible because the order of arguments doesn’t matter.

{% stepper %}
{% step %}
### Basic Keyword Arguments

```python
def introduce(name, age):
    print(f"My name is {name} and I am {age} years old.")

introduce(name="Suraj", age=30)
introduce(age=30, name="Suraj")  # Order doesn't matter

# Output:
# My name is Suraj and I am 30 years old.
# My name is Suraj and I am 30 years old.
```

Note: Use keyword arguments to avoid mistakes with argument order.
{% endstep %}

{% step %}
### Keyword Arguments with Default Values

```python
def greet(name="Guest", language="English"):
    print(f"Hello {name}, welcome! (Language: {language})")

greet()                               # Uses both defaults
greet(name="Suraj")                   # Only language uses default
greet(language="Hindi")               # Only name uses default
greet(name="Suraj", language="Hindi") # Both provided

# Output:
# Hello Guest, welcome! (Language: English)
# Hello Suraj, welcome! (Language: English)
# Hello Guest, welcome! (Language: Hindi)
# Hello Suraj, welcome! (Language: Hindi)
```
{% endstep %}

{% step %}
### Mixing Positional and Keyword Arguments

NOTE: Positional arguments must come first, then keyword arguments.

```python
def describe_pet(pet_type, pet_name):
    print(f"I have a {pet_type} named {pet_name}.")

describe_pet("dog", "Buddy")                      # Positional
describe_pet(pet_name="Buddy", pet_type="dog")   # Keyword

# Output:
# I have a dog named Buddy.
# I have a dog named Buddy.
```
{% endstep %}

{% step %}
### Arbitrary Positional Arguments (\*args)

Definition: Use `*args`  when you want a function to accept any number of positional arguments. They are collected as a tuple.

Example 1 - Sum Numbers:

```python
def add_numbers(*args):
    total = 0
    for num in args:
        total += num
    return total

print(add_numbers(2, 3, 5))          # Output: 10
print(add_numbers(1, 2, 3, 4, 5))    # Output: 15
```

Example 2 - Print all items:

```python
def print_items(*items):
    for item in items:
        print(item)

print_items("apple", "banana", "cherry")
```

Note: Use `*args` for extra positional arguments you don’t know in advance.
{% endstep %}

{% step %}
### Arbitrary Keyword Arguments (\*\*kwargs)

Definition: Use `**kwargs`  when you want a function to accept any number of keyword arguments. They are collected as a dictionary.

Example A:

```python
def print_info(**info):
    for key, value in info.items():
        print(f"{key}: {value}")

print_info(name="Suraj", age=30, city="Kanpur")

# Output:
# name: Suraj
# age: 30
# city: Kanpur
```

Example B -  Mix regular and arbitrary keyword arguments:

```python
def greet(message, **person):
    print(message)
    for key, value in person.items():
        print(f"{key}: {value}")

greet("Welcome!", name="Suraj", age=30)

# Output:
# Welcome!
# name: Suraj
# age: 30
```

Note: Use `**kwargs` for flexible functions where you don’t know all parameter names in advance.
{% endstep %}

{% step %}
### Combining \*args and \*\*kwargs

NOTE: `*args` must come before `**kwargs`.

Example 1 - Simple combination:

```python
def show_info(*args, **kwargs):
    print("Positional arguments:", args)
    print("Keyword arguments:", kwargs)

show_info(1, 2, 3, name="Suraj", age=19)

# Output:
# Positional arguments: (1, 2, 3)
# Keyword arguments: {'name': 'Suraj', 'age': 19}
```

Example 2 - With regular parameters:

```python
def order(item, *args, **kwargs):
    print("Item:", item)
    print("Additional info:", args)
    print("Other details:", kwargs)

order("Book", "Hardcover", "Red cover", quantity=3, price=50)

# Output:
# Item: Book
# Additional info: ('Hardcover', 'Red cover')
# Other details: {'quantity': 3, 'price': 50}
```
{% endstep %}
{% endstepper %}

## Recursion

Definition: Recursion is a technique where a function calls itself to solve a problem. It's useful for problems that can be divided into smaller similar subproblems.

Structure of a Recursive Function:

```python
def recursive_function(parameters):
    if base_case_condition:
        # Stop condition
        return something
    else:
        return recursive_function(smaller_problem)
```

Example 1 — Factorial:

```python
def factorial(n):
    if n == 0:        # Base case
        return 1
    else:
        return n * factorial(n-1)  # Recursive call

print(factorial(5))  # Output: 120
```

Example 2 — Fibonacci Sequence:

```python
def fibonacci(n):
    if n == 0:
        return 0
    elif n == 1:
        return 1
    else:
        return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(6))  # Output: 8
```

Note: Always define a base case, otherwise the recursion will run infinitely.

## Lambda Functions (Anonymous Functions)

Definition: A lambda function is a small anonymous function defined using the keyword `lambda`. It can take any number of arguments but only has a single expression.

Syntax:

```python
lambda arguments: expression
```

Example 1 — Basic Lambda:

```python
square = lambda x: x**2
print(square(5))  # Output: 25
```

Example 2 — Lambda with Multiple Arguments:

```python
add = lambda a, b: a + b
print(add(3, 7))  # Output: 10
```
