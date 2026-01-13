---
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# String CheatSheet

{% stepper %}
{% step %}
### Concatenation (+)

It joins a string with another string.

```python
str1 = 'hi I am'
str2 = 'ayush'
result = str1 + str2  # 'hi I amayush'
```
{% endstep %}

{% step %}
### Repetition (\*)

It repeats a string.

```python
str = 'ayush'
result = str * 3  # 'ayushayushayush'
```
{% endstep %}

{% step %}
### Membership operator: in / not in

* in: checks presence of a substring in a string.
* not in: checks absence of a substring in a string.

```python
str1 = 'hi I am Ayush'
result = 'I' in str1   # True

str1 = 'hi I am Ayush'
result = 'z' in str1   # False
```
{% endstep %}

{% step %}
### len()

Gives the length (number of characters) of the string.

```python
str1 = 'hi i am Ayush'
result = len(str1)  # 13
```
{% endstep %}

{% step %}
### max()

Gives the maximum value character in a string.

```python
str1 = 'Ayush'
result = max(str1)  # 'y'
```
{% endstep %}

{% step %}
### min()

Gives the minimum value character in a string.

```python
str1 = 'Ayush'
result = min(str1)  # 'A'
```
{% endstep %}

{% step %}
### .lower()

Converts all characters of a string to lower case.

```python
str1 = 'AYUSH'
result = str1.lower()  # 'ayush'
```
{% endstep %}

{% step %}
### .upper()

Converts all characters of a string to upper case.

```python
str1 = 'ayush'
result = str1.upper()  # 'AYUSH'
```
{% endstep %}

{% step %}
### .capitalize()

Capitalizes the first character of the string only.

```python
str1 = 'HI I AM AYUSH'
result = str1.capitalize()  # 'Hi i am ayush'
```
{% endstep %}

{% step %}
### .title()

Capitalizes the first letter of each word in the string.

```python
str1 = 'HI I AM AYUSH'
result = str1.title()  # 'Hi I Am Ayush'
```
{% endstep %}

{% step %}
### .swapcase()

Converts lowercase characters to uppercase and uppercase to lowercase.

```python
str1 = ' Hi I aM aYUsh'
result = str1.swapcase()  # 'hI i Am AyuSH'
```
{% endstep %}

{% step %}
### .strip()

Removes whitespace from left and right sides of the string.

```python
str1 = ' ayush '
result = str1.strip()  # 'ayush'
```
{% endstep %}

{% step %}
### .lstrip()

Removes whitespace from the left side only.

```python
str1 = ' ayush '
result = str1.lstrip()  # 'ayush '  (spaces on right remain)
```
{% endstep %}

{% step %}
### .rstrip()

Removes whitespace from the right side only.

```python
str1 = ' ayush '
result = str1.rstrip()  # ' ayush'  (spaces on left remain)
```
{% endstep %}

{% step %}
### .replace(old, new)

Replaces all occurrences of the old substring with the new substring.

```python
str1 = 'python is python and python is good.'
result = str1.replace('Python', 'java')  # Note: case-sensitive
# result: 'python is python and python is good.' (no change due to case)
```

Also:

```python
str1 = 'python is python and python is good'
result = str1.replace('python', 'java', 2)
# 'java is java and python is good.'
```
{% endstep %}

{% step %}
### .count('substring')

Gives the count of a substring in the string.

```python
str1 = 'python is python and python is good'
result = str1.count('o')  # 5
```

Also with start/end:

```python
str1 = 'python is python and python is good'
result = str1.count('o', 15, 35)  # 3
```
{% endstep %}

{% step %}
### .find('substring')

Gives the index of the first appearance of the substring (or -1 if not found).

```python
str1 = 'python is python and python is good'
result = str1.find('y')  # 1
```

With start/end:

```python
str1 = 'python is python'
result = str1.find('y', 2, 15)  # 11
```
{% endstep %}

{% step %}
### .rfind('substring')

Gives the index of the first appearance of the substring searching from the right.

```python
str1 = 'python is python'
result = str1.rfind('y')  # 11
```
{% endstep %}

{% step %}
### .index('substring')

Gives the index of the first appearance of the substring (raises ValueError if not found).

```python
str1 = 'python is python and python is good'
result = str1.index('y')  # 1
```

With start/end:

```python
str1 = 'python is python'
result = str1.index('y', 2, 15)  # 11
```
{% endstep %}

{% step %}
### .rindex('substring')

Gives the index of the first appearance of the substring from the right (raises ValueError if not found).

```python
str1 = 'python is python'
result = str1.rindex('y')  # 11
```
{% endstep %}

{% step %}
### .split(separator)

Breaks a string into a list of substrings using the separator. Default separator is space.

```python
str1 = 'python is a programming language'
result = str1.split()  # ['python', 'is', 'a', 'programming', 'language']
```

With maxsplit:

```python
str1 = 'python is a programming language'
result = str1.split(' ', 2)  # ['python', 'is', 'a programming language']
```
{% endstep %}

{% step %}
### .rsplit(separator)

Breaks a string into a list of substrings using the separator, starting from the right. Default separator is space.

```python
str1 = 'python is a programming language'
result = str1.rsplit()  # ['python', 'is', 'a', 'programming', 'language']
```

With maxsplit:

```python
str1 = 'python is a programming language'
result = str1.rsplit(' ', 2)  # ['python is a', 'programming', 'language']
```
{% endstep %}

{% step %}
### .partition()

Splits the string at the first occurrence of the separator and includes the separator in the output.

```python
str1 = 'python is a programming language'
result = str1.partition(' ')  # ('python', ' ', 'is a programming language')
```

Also:

```python
str1 = 'python is a programming language'
result = str1.rpartition(' ')  # ('python is a programming', ' ', 'language')
```
{% endstep %}

{% step %}
### .islower()

Checks whether all alphabetic characters in the string are lowercase.

```python
str1 = 'ayush'
result = str1.islower()  # True
```
{% endstep %}

{% step %}
### .isupper()

Checks whether all alphabetic characters in the string are uppercase.

```python
str1 = 'AYUSH'
result = str1.isupper()  # True
```
{% endstep %}

{% step %}
### .alpha()

Checks whether all characters in a string are alphabetic.

```python
str1 = 'ayush'
result = str1.alpha()  # True
```

Note: the original example uses .alpha() as shown.
{% endstep %}

{% step %}
### .isnumeric()

Checks whether all characters in a string are numeric digits.

```python
str1 = '12345'
result = str1.isnumeric()  # True
```
{% endstep %}

{% step %}
### .isalnum()

Checks whether all characters in a string are alphabetic or digits only.

```python
str1 = 'ayush12345'
result = str1.isalnum()  # True
```
{% endstep %}

{% step %}
### .startswith()

Checks whether the string starts with a particular substring.

```python
str1 = '+91 1234567890'
result = str1.startswith('+91')  # True
```
{% endstep %}

{% step %}
### .endswith()

Checks whether the string ends with a particular substring.

```python
str1 = 'myfile.txt'
result = str1.endswith('txt')  # True
```
{% endstep %}

{% step %}
### .isspace()

Checks whether the string contains only whitespace characters (space, tab, newline).

```python
str1 = " "
result = str1.isspace()  # True
```
{% endstep %}

{% step %}
### .istitle()

Checks whether the string follows title case (first letter of each word capital.

```python
str1 = "Hi I Am Shikher"
str1 = "Hi I Am Shikher"
result = str1.istitle()  # True

str2 = "This is Python programming"
result = str2.istitle()  # False
```


{% endstep %}

{% step %}
### .center(width, fillchar)

Centers the string by adding characters on both sides.

```python
str2 = "Ayush"
result = str2.center(10, '*')  # **Ayush***
```

Explanation of parameters:

* width → Total length of the final string
* fillchar → Character used to fill empty spaces (must be one character)
{% endstep %}

{% step %}
### .ljust(width, fillchar)

Aligns the string to the left and fills the right side.

```python
str2 = "Ayush"
result = str2.ljust(10, '-')  # Ayush-----
```

Explanation of parameters:

* width → Total length of the final string
* fillchar → Character used to fill empty spaces (must be one character)


{% endstep %}

{% step %}
### .rjust(width, fillchar)

Aligns the string to the right and fills the left side.

```python
str2 = "Ayush"
result = str2.rjust(10, '-')  # -----Ayush
```

Explanation of parameters:

* width → Total length of the final string
* fillchar → Character used to fill empty spaces (must be one character)


{% endstep %}
{% endstepper %}

## String Formatting ( f" " )&#x20;

Allows embedding variables directly inside strings using {}.

```python
# Basic Example
name = "Ayush"
age = 61
print(f"My name is{name} and age is{age}")  # My name is Ayush and my age is 61
```

```python
# Expression inside f-string
a = 10
b = 5
print(f"Sum is{a+b}")
```

## String Slicing&#x20;

```python
str1 = "Programming"
```

Default Slicing:

```python
str1[::]  # 'Programming'
```

Positive Index Slicing:

```python
str1[0:6]  # 'Progra'
```

Negative Index Slicing:

```python
str1[-7:-1]  # 'ammin'
```

Mixed Index Slicing:

```python
str1[3:-3]  # 'gramm'
```

Slicing with Step:

```python
str1[::2]  # 'Pormig'
```

Reverse String (Negative Step):

```python
str1[::-1]  # 'gnimmargorP'
```

## Escape Characters&#x20;

\n — New Line: Moves the cursor to the next line.

```python
print("Hello\nWorld")
# Hello
# World
```

\t — Tab Space: Adds horizontal tab space (used for alignment).

```python
print("Name\tMarks")  # Name    Marks
print("Ayush\t95")    # Ayush   95
```

\ — Backslash: Used to print a single backslash.

```python
print("C:\\Users\\Ayush")  # C:\Users\Ayush
```

\\' — Single Quote: Used to print a single quote inside single-quoted string.

```python
print('It\'s a Python class')  # It's a Python class
```

\\" — Double Quote: Used to print a double quote inside double-quoted string.

```python
print("He said\"Python is easy\"")  # He said "Python is easy"
```
