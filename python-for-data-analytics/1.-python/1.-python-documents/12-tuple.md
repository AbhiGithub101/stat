# 15. Tuple

{% embed url="https://youtu.be/fHxHwqjCBA0" %}

#### What are Tuples? <a href="#what-is-tuples" id="what-is-tuples"></a>

Tuples are used to store multiple items in a single variable. It is also an iterable.

In simpler terms, a tuple is a collection of items enclosed between Parantheses ().

Properties: Ordered, immutable(unchangeable), Allow Duplicate Values.

For Example:

In \[1]:

```
name = ('Mark','Bill','Elon')
print(name)
```

#### Memory Allocation of Tuple items: <a href="#memory-allocation-of-tuple-items" id="memory-allocation-of-tuple-items"></a>

As we know that Tuples is a sequence of items, hence Each item of Tuple gets store in different memory block, similar to list.

#### Indexing and Slicing in Tuple: <a href="#indexing-and-slicing-in-tuple" id="indexing-and-slicing-in-tuple"></a>

Indexing and Slicing in Tuple is also similar to list. For Example:

In \[2]:

```
#indexing in Tuple:
name = ('Mark','Bill','Elon')
name[1]
```

In \[3]:

```
name = ('Mark','Bill','Elon')
name[-1]
```

In \[4]:

```
#Slicing in Tuple:
name = ('Mark','Bill','Elon')
name[0:2]
```

#### Properties of a Tuple: <a href="#properties-of-a-tuple" id="properties-of-a-tuple"></a>

1. **Tuples are Ordered:**

When you define a Tuple, its items are stored and assigned to a specific index number. It means Tuple items are ordered. To explain it better, here is an Example:

In \[7]:

```
vartuple = ("console","flare","python","data")
print(vartuple)
```

```
('console', 'flare', 'python', 'data')
```

2. **Tuples are Immutable/UnChangeable:**

We cannot change the items in a tuple once defined.

In \[8]:

```
vartuple = ("console","flare","python","data")
vartuple[3] = "data science"
```

```
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-8-452a68df3a1c> in <module>
      1 vartuple = ("console","flare","python","data")
----> 2 vartuple[3] = "data science"

TypeError: 'tuple' object does not support item assignment
```

3. **Tuples allow duplicate values:**

A tuple allows duplicate values; it can have as many duplicate values. For Example:

In \[9]:

```
vartuple = ("console","flare","python","data","data")
print(vartuple)
```

```
('console', 'flare', 'python', 'data', 'data')
```

#### Functions used in Tuple : <a href="#functions-used-in-tuple" id="functions-used-in-tuple"></a>

**len() function:**

len() function is used to count items in a Tuple. For Example:

In \[10]:

```
vartuple = ("console","flare","python","data")
len(vartuple)
```

**max() function:**

max() function is used to return largest value or item in a Tuple ,For Example:

In \[11]:

```
vartuple = [23,45,12,76,83]
max(vartuple)
```

In \[12]:

```
vartuple = [23,45,12,76,83]
min(vartuple)
```

**max() and min() functions do not work on mixed Tuples with different data types, just like Lists.**

### Tuple Operations: <a href="#tuple-operations" id="tuple-operations"></a>

**how to Concatenate two Tuples** $$+$$**:**

```
vartuple = (1,2,3,4,5,6,7,8,9)
anothertuple = ('a','b','c','d')
combined_tuple = vartuple + anothertuple
print(combined_tuple)
```

```
(1, 2, 3, 4, 5, 6, 7, 8, 9, 'a', 'b', 'c', 'd')
```

**Repetition of two Tuples** $$∗$$**:**

```
var_tuple = (1,2,3,4,5,6,7,8,9)
rep_tuple = var_tuple * 2
print(rep_tuple)
```

```
(1, 2, 3, 4, 5, 6, 7, 8, 9, 1, 2, 3, 4, 5, 6, 7, 8, 9)
```

**Membership operator in Tuples:**

```
var_tuple = [1,2,3,4,5,6,7,8,9]
present = 1 in var_tuple
print(present)
```

```
True
```

### iteration in tuples:

For loop is used to iterate over the Tuple items. For example:

```
var_tuple = (1,2,3,4,5,6,7,8,9)

for i in var_tuple:
    print(i)
```

```
1
2
3
4
5
6
7
8
9
```

### Empty Tuple:

We can create an empty tuple with the help of parentheses().

```
empty_tuple = ()
print(empty_tuple)
```

```
()
```

### To create a tuple with a single item:

In a tuple, you can not simply create a tuple with a single item. For example:

```
var = (5)
type(var)
```

```
int
```

Now, here var is not a tuple, it is an integer because Python treats parentheses here as an operator. So What is the Solution?

```
var = (5,)
type(var)
```

```
tuple
```

So, we can create a tuple with a single item by using a comma like above.

### Tuple Methods:

Since we cannot change values in a tuple once we have defined it. So there are only two methods in Tuple.

### 1.count() :

Count method is used to count occurence of elements in Tuples.

```
var = (1,2,3,4,4,4,4,4)
x = var.count(4)
print(x)
```

```
5
```

### 2.index() :

The index method is used to find the position of an element in a tuple.

```
var = ("console","flare","python","data")
position = var.index("data")
print(position)
```

```
3
```

### tuple() Constructor :

A tuple constructor is used to convert an iterable to a tuple. We can also use it to create an empty tuple.

```
varlist = [1,2,3,4]
vartuple = tuple(varlist)
print(vartuple)
```

```
(1, 2, 3, 4)
```

```
var = "Console"
var = tuple(var)
print(var)
```

```
('C', 'o', 'n', 's', 'o', 'l', 'e')
```

```
#To Create an empty tuple.
var = tuple()
print(var)
```

```
()
```
