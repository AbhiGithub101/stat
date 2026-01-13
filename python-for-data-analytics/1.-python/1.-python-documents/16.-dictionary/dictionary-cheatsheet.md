---
description: Complete Python Dictionary cheatsheet with clear examples for quick revision
---

# Dictionary Cheatsheet

Example: `my_dict = {'name': 'John', 'age': 25, 'city': 'New York'}`

{% stepper %}
{% step %}
#### clear()

Removes all items from the dictionary.

```python
my_dict.clear()  # {}
```
{% endstep %}

{% step %}
#### copy()

Creates a copy of a dictionary.

```python
new_dict = my_dict.copy()  # {'name':'John', 'age':25, 'city':'New York'}
```
{% endstep %}

{% step %}
#### get()

Returns the value of a particular key.

```python
my_dict.get('age')  # 25
```
{% endstep %}

{% step %}
#### items()

Returns all the items present in the dictionary as (key, value) pairs.

```python
my_dict.items()  # (name, john), (age, 25), (city, New York)
```
{% endstep %}

{% step %}
#### keys()

Returns a list of keys in a dictionary.

```python
my_dict.keys()  # [name, age, city]
```
{% endstep %}

{% step %}
#### values()

Returns a list of values in a dictionary.

```python
my_dict.values()  # [john, 25, new york]
```
{% endstep %}

{% step %}
#### pop(key)

Removes the key-value pair from the dictionary.

```python
my_dict.pop('age')  # {'name': 'John', 'city': 'New York'}
```
{% endstep %}

{% step %}
#### popitem()

Removes the last key-value pair from the dictionary.

```python
my_dict.popitem()  # {'name': 'John', 'age': 25}
```
{% endstep %}

{% step %}
#### update()

Updates a dictionary by adding the items from another dictionary.

```python
new_dict = {'country':'USA', 'mob_num':12345}
my_dict.update(new_dict)
# {'name': 'John', 'age': 25, 'city': ' New York', 'country':'USA', 'mob_num':12345}
```
{% endstep %}

{% step %}
#### setdefault(key, value)

Returns the value for a key if it exists. If not, inserts the key with a value of default and returns default.

```python
my_dict.setdefault('age', 30)   # {'name': 'John', 'age': 25, 'city': 'New York'}
my_dict.setdefault('height', 175)  # {'name': 'John', 'age': 25, 'city': 'New York', 'height', 175}
```
{% endstep %}

{% step %}
#### fromkeys()

Creates a new dictionary with keys from iterable and values set to value.

```python
new_dict = dict.fromkeys(['a', 'b', 'c'], 0)  # {'a': 0, 'b': 0, 'c': 0}
```
{% endstep %}
{% endstepper %}
