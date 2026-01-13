---
description: Complete Python List cheatsheet with clear examples for quick revision
---

# List Cheatsheet

{% stepper %}
{% step %}
### append(item)

To add an item to a list.

```python
l1 = [12, 23, 34, 56]
l1.append(3.14)  # [12, 23, 34, 56, 3.14]
```
{% endstep %}

{% step %}
### extend(list)

To add all elements of another list to a list.

```python
l1 = [12, 23, 34, 56]
l2 = ['a', 'b', 'c']
l1.extend(l2)  # [12, 23, 34, 56, 'a', 'b', 'c']
```
{% endstep %}

{% step %}
### insert(index, item)

To add an item at a particular index in a list.

```python
l1 = [12, 23, 34, 56]
l1.insert(2, 420)  # [12, 23, 420, 34, 56]
```
{% endstep %}

{% step %}
### remove(item)

To remove the first occurrence of an item from the list.

```python
l1 = [12, 23, 34, 56]
l1.remove(34)  # [12, 23, 56]
```
{% endstep %}

{% step %}
### pop(index)

To remove an item from the list by index and return it.

```python
l1 = [12, 23, 34, 56]
l1.pop(1)  # returns 23, l1 becomes [12, 34, 56]
```
{% endstep %}

{% step %}
### index(item)

Returns the index of the first matching item.

```python
l1 = [12, 23, 34, 56]
l1.index(23)  # 1
```
{% endstep %}

{% step %}
### count(item)

Returns how many times an item appears in the list.

```python
l1 = [12, 23, 34, 56, 34, 34]
l1.count(34)  # 3
```
{% endstep %}

{% step %}
### sort()

Sorts the list in ascending order in place.

```python
l1 = [90, 121, 1, 2, 23, 34, 5, 6]
l1.sort()  # [1, 2, 5, 6, 23, 34, 90, 121]
```
{% endstep %}

{% step %}
### reverse()

Reverses the items of the list in place.

```python
l1 = [90, 121, 1, 2, 23, 34, 5, 6]
l1.reverse()  # [6, 5, 34, 23, 2, 1, 121, 90]
```
{% endstep %}

{% step %}
### copy()

Returns a shallow copy of the list.

```python
l1 = [90, 121, 1, 2, 23, 34, 5, 6]
l2 = l1.copy()  # [90, 121, 1, 2, 23, 34, 5, 6]
```
{% endstep %}

{% step %}
### clear()

Removes all items from the list.

```python
l1 = [90, 121, 1, 2, 23, 34, 5, 6]
l1.clear()  # []
```
{% endstep %}
{% endstepper %}
