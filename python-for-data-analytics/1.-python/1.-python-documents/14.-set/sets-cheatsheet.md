---
description: Complete Python Sets cheatsheet with clear examples for quick revision
---

# Sets Cheatsheet

{% stepper %}
{% step %}
#### .add(item)

Adds a single item to a set.

{% code title="example" %}
```python
s1 = {12, 34, 23, 56, 78, 45}
s1.add(3.14)  # {12, 34, 23, 56, 78, 45, 3.14}
```
{% endcode %}
{% endstep %}

{% step %}
#### .update(iterable)

Updates a set by adding elements from an iterable (list, set, tuple).

{% code title="example" %}
```python
s1 = {12, 34, 23, 56, 78, 45}
s1.update([1.23, 4.20, 5.67])  # {12, 1.23, 23, 34, 4.20, 45, 56, 78, 5.67}
```
{% endcode %}
{% endstep %}

{% step %}
#### .union(set)

Returns a new set consisting of items from both sets.

{% code title="example" %}
```python
s1 = {12, 34, 23, 56, 78, 45}
s2 = {1.23, 4.20, 5.67}
s1.union(s2)  # {12, 1.23, 23, 34, 4.20, 45, 56, 78, 5.67}
```
{% endcode %}
{% endstep %}

{% step %}
#### .remove(item)

Removes a specific item from the set. (Raises KeyError if the item is not present.)

{% code title="example" %}
```python
s1 = {12, 34, 23, 56, 78, 45}
s1.remove(56)  # {12, 34, 23, 78, 45}
```
{% endcode %}
{% endstep %}

{% step %}
#### .discard(item)

Removes a specific item from the set. (Does nothing if the item is not present.)

{% code title="example" %}
```python
s1 = {12, 34, 23, 56, 78, 45}
s1.discard(34)  # {12, 23, 56, 78, 45}
```
{% endcode %}
{% endstep %}

{% step %}
#### .pop()

Removes and returns an arbitrary item from the set.

{% code title="example" %}
```python
s1 = {12, 34, 23, 56, 78, 45}
s1.pop()  # removes and returns an arbitrary item
# resulting set might be {12, 34, 23, 56, 45} (actual item removed is arbitrary)
```
{% endcode %}
{% endstep %}

{% step %}
#### .clear()

Removes all the items from the set.

{% code title="example" %}
```python
s1 = {12, 34, 23, 56, 78, 45}
s1.clear()  # set()
```
{% endcode %}
{% endstep %}

{% step %}
#### .copy()

Returns a shallow copy of the set.

{% code title="example" %}
```python
s1 = {12, 34, 23, 56, 78, 45}
s2 = s1.copy()  # s2 = {12, 34, 23, 56, 78, 45}
```
{% endcode %}
{% endstep %}

{% step %}
#### .intersection(set)

Returns a new set with items common to both sets.

{% code title="example" %}
```python
s1 = {12, 34, 23, 56, 78, 45}
s2 = {1, 2, 34, 56, 78, 9, 11}
s1.intersection(s2)  # {34, 56, 78}
```
{% endcode %}
{% endstep %}

{% step %}
#### .difference(set)

Returns a new set with the items in the first set but not in the second.

{% code title="example" %}
```python
s1 = {12, 34, 23, 56, 78, 45}
s2 = {1, 2, 34, 56, 78, 9, 11}
s1.difference(s2)  # {12, 23, 45}
```
{% endcode %}
{% endstep %}

{% step %}
#### .symmetric\_difference(set)

Returns a new set with items that are in either set but not in both (uncommon items).

{% code title="example" %}
```python
s1 = {12, 34, 23, 56, 78, 45}
s2 = {1, 2, 34, 56, 78, 9, 11}
s1.symmetric_difference(s2)  # {12, 23, 45, 1, 2, 9, 11}
```
{% endcode %}
{% endstep %}
{% endstepper %}
