# 15. Tuple

#### What is Tuples? <a href="#what-is-tuples" id="what-is-tuples"></a>

Tuples are used to store multiple items in a single variable. It is also an iterable.

In more simpler terms, Tuple is a collection of items enclosed between Parantheses ().

Properties : Ordered , immutable(unchangeable) , Allow Duplicate Values.

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

**1.Tuples are Ordered:**

When You define a Tuple , its items are stored and assigned to specific index number. It means Tuple items are ordered . To Explain it better, Here is an Example:

In \[7]:

```
vartuple = ("console","flare","python","data")
print(vartuple)
```

```
('console', 'flare', 'python', 'data')
```

**1.Tuples are Immutable/UnChangeable:**

We cannot change the items in Tuple once defined.

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

**3.Tuples allow duplicate values:**

Tuple allows duplicate values, it can have as many duplicate values. For Example:

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

**max() and min() function does not work in mixed Tuples with different category of data types , Just like Lists.**

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

for loop is used to iterate over the Tuple items. For example:

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

We can create an empty tuple with the help of parantheses ().

```
empty_tuple = ()
print(empty_tuple)
```

```
()
```

### To create a tuple with Single item:

In tuple , You can not simply create a tuple with single item. For example:

```
var = (5)
type(var)
```

```
int
```

Now , here var is not a tuple , it is an integer because python treats parantheses here as Operator. So What is the Solution?

```
var = (5,)
type(var)
```

```
tuple
```

So , We can create a tuple with single item by using comma like above.

### Tuple Methods:

Since We cannot change values in Tuple once we have defined tuple. So there are only two methods in Tuple.

### 1.count() :

count method is used to count occurence of elements in Tuples.

```
var = (1,2,3,4,4,4,4,4)
x = var.count(4)
print(x)
```

```
5
```

### 2.index() :

index method is used to find position of element in tuple.

```
var = ("console","flare","python","data")
position = var.index("data")
print(position)
```

```
3
```

### tuple() Constructor :

tuple constructor is used to convert an iterable to tuple. We can also use to create an empty tuple with it.

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
