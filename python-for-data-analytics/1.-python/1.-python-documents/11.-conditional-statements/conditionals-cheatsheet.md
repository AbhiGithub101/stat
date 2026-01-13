---
description: Complete Python Conditionals cheatsheet with clear examples for quick revision
---

# Conditionals Cheatsheet

> Conditionals are used to make decisions in a program based on True / False conditions. Python uses several forms of conditionals:

{% stepper %}
{% step %}
### if Statement

Used to execute code only when a condition is **True**.\
Note : Condition must evaluate to True or False. Indentation is mandatory in Python.

{% code title="if_statement.py" %}
```python
# if Statement Example
age = 18
if age >= 18:  # condition is True
    print("You are eligible to vote")
# NOTE -> if condition is False, there will be no output
```
{% endcode %}

{% hint style="info" %}
Indentation is required to define the block that runs when the condition is True.
{% endhint %}
{% endstep %}

{% step %}
### if-else Statement

Used when you want two possible outcomes.

{% code title="if_else_example.py" %}
```python
# if-else Example
num = int(input("Enter a number: "))
if num % 2 == 0:
    print("Even number")
else:
    print("Odd number")

# Examples:
# num = 4 -> Output: Even number
# num = 9 -> Output: Odd number
# Note: else runs only when if condition is False
```
{% endcode %}
{% endstep %}

{% step %}
### Short-hand (Ternary) if

Used for single-line conditions.

{% code title="ternary_example.py" %}
```python
a = 5
b = 10
max_value = a if a > b else b
print(max_value)
```
{% endcode %}

{% hint style="info" %}
Best for single condition + single action. Becomes confusing for complex logic.
{% endhint %}
{% endstep %}

{% step %}
### if-elif-else Statement

Used to check multiple conditions.

{% code title="if_elif_else.py" %}
```python
marks = 72
if marks >= 90:
    print("Grade A")
elif marks >= 75:
    print("Grade B")
elif marks >= 50:
    print("Grade C")
else:
    print("Fail")

# Note:
# 1. Python checks conditions top to bottom
# 2. Only one block runs
```
{% endcode %}
{% endstep %}

{% step %}
### Nested Conditions

A condition inside another condition.

#### Example 1

{% code title="nested_example1.py" %}
```python
num = 10
if num > 0:
    if num % 2 == 0:
        print("Even Number")
    else:
        print("Odd Number")
else:
    print("Negative Number")
```
{% endcode %}

#### Example 2

| Marks     | Attendance | Result | Grade | Scholarship |
| --------- | ---------- | ------ | ----- | ----------- |
| `< 40`    | Any        | Fail   | F     | No          |
| `40 – 59` | Any        | Pass   | C     | No          |
| `60 – 84` | Any        | Pass   | B     | No          |
| `≥ 85`    | `< 75`     | Pass   | A     | No          |
| `≥ 85`    | `≥ 75`     | Pass   | A     | Yes         |

{% code title="nested_example2.py" %}
```python
marks = int(input("Enter marks: "))
attendance = int(input("Enter attendance percentage: "))

if marks >= 40:  # First condition (pass/fail)
    print("Result: Pass")
    if marks >= 85:  # Nested if-elif-else
        if attendance >= 75:
            print("Grade: A")
            print("Scholarship: Eligible")
        else:
            print("Grade: A")
            print("Scholarship: Not eligible (low attendance)")
    elif marks >= 60:
        print("Grade: B")
        print("Scholarship: Not eligible")
    else:
        print("Grade: C")
        print("Scholarship: Not eligible")
else:
    print("Result: Fail")
    print("Grade: F")
```
{% endcode %}
{% endstep %}

{% step %}
### pass Statement

Used when a condition is required syntactically but no action is needed.

{% code title="pass_example.py" %}
```python
if age > 18:
    pass
```
{% endcode %}
{% endstep %}
{% endstepper %}
