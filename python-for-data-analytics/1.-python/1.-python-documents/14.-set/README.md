# 14. Set

### What are sets? <a href="#what-are-sets" id="what-are-sets"></a>

A Python set is the collection of the unordered items. Each element in the set must be unique, immutable, and the sets remove the duplicate elements. Sets are mutable which means we can modify it after its creation.

Properties : Unordered , Mutable\Changeable , Does not allow Duplicate Values.

Sets are unordered and its item has no index numbers. It means Index numbers do not exist in Sets.

Set items are defined in enclosed curly braces {}. For Example:

In \[1]:

```
varset = {"Console","Python","data","Flare"}
print(varset)
```

```
{'data', 'Python', 'Console', 'Flare'}
```

#### Properties of Sets: <a href="#properties-of-sets" id="properties-of-sets"></a>

#### 1.Sets are Unordered : <a href="#id-1.sets-are-unordered" id="id-1.sets-are-unordered"></a>

In sets , items of set has no index number . So there is no order in element of sets. For Example:

In \[1]:

```
varset = {"Console","Python","data","Flare"}
print(varset)
```

```
{'Python', 'data', 'Flare', 'Console'}
```

In \[4]:

```
varset = {"Console","Python","data","Flare"}
print(varset) 
```

```
{'Python', 'Flare', 'data', 'Console'}
```

So from the above codes , we can figure out that there is no order in sets and items of sets have no specific position because there is no index numbers associated with set items.

#### Indexing and Slicing in Sets: <a href="#indexing-and-slicing-in-sets" id="indexing-and-slicing-in-sets"></a>

Because set has no indexes , so there is no indexing or slicing in set. We cannot access any particular set item. For Example:

In \[5]:

```
varset = {"Console","Python","data","Flare"}
varset[1]
```

```
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-5-a3fa81f31623> in <module>
      1 varset = {"Console","Python","data","Flare"}
----> 2 varset[1]

TypeError: 'set' object is not subscriptable
```

#### Sets are Mutable : <a href="#sets-are-mutable" id="sets-are-mutable"></a>

Sets are Changeable , we can add or remove values in a set by using set method. For Example:

In \[6]:

```
varset = {"Console","Python","data","Flare"}
varset.add("Science")
print(varset)
```

```
{'data', 'Flare', 'Science', 'Python', 'Console'}
```

#### Sets do not allow duplicate values : <a href="#sets-do-not-allow-duplicate-values" id="sets-do-not-allow-duplicate-values"></a>

Sets remove duplicate values and keeps only one value in set.For Example :

In \[7]:

```
varset = {"Console","Python","data","Flare","Flare","Flare","Flare"}
print(varset)
```

```
{'Python', 'data', 'Flare', 'Console'}
```

Though we inserted 3 'Flare' in set, set will have only one 'Flare' as a single item.

#### Functions used in sets: <a href="#functions-used-in-tuple" id="functions-used-in-tuple"></a>

**Just like other iterables (string , list , tuple) , Functions in sets are same.**

In \[9]:

```
varset = {"Console","Python","data","Flare"}
max(varset)
```

In \[10]:

```
varset = {"Console","Python","data","Flare"}
min(varset)
```

In \[11]:

```
varset = {"Console","Python","data","Flare"}
len(varset)
```

#### Type of a set: <a href="#type-of-a-set" id="type-of-a-set"></a>

In \[1]:

```
varset = {1,2,3}
type(varset)
```

**Membership operator in set:**

In \[7]:

```
var_set = {1,2,3,4,5,6,7,8,9}
present = 1 in var_set
print(present)
```

#### Set Methods: <a href="#set-methods" id="set-methods"></a>

Functions that are specific to Set are known as Set methods. We will go through each method one by one.

#### Adding an item or a single element in a set: add() <a href="#adding-an-item-or-a-single-element-in-a-set-add" id="adding-an-item-or-a-single-element-in-a-set-add"></a>

By now we have read other data structures like list , tuples. To add an item or a single element in list , we would use append method , but in set we use add() method. There is not much difference between both.

add() method does not return any value and adds element in set.

**Note:**&#x42;ecause sets have no index number, elements that we add in set position themselves in random place.

In \[18]:

```
var_set = {1,2,3,4,5,6,'console',7,8,9}
var_set.add("flare")
print(var_set)
```

```
{1, 2, 3, 4, 5, 6, 7, 8, 9, 'flare', 'console'}
```

Just like append() , add() method also treats parameters as a single element. so if we try to add an iterable through add() method , it will be added in set as a single element. For Example:

In \[19]:

```
var_set = {1,2,3,4,5,6,'console',7,8,9}
var_set.add(('Python','Data Science'))
print(var_set)
```

```
{1, 2, 3, 4, 5, 6, 7, 8, 9, 'console', ('Python', 'Data Science')}
```

**Note:**&#x57;e are not allowed to add a mutable data structures in a set. hence Lists , sets , Dictionary and sets are not allowed in a set.

In \[20]:

```
var_set = {1,2,3,4,5,6,'console',7,8,9}
var_set.add([10,11])
print(var_set)
```

```
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-20-ba1263667386> in <module>
      1 var_set = {1,2,3,4,5,6,'console',7,8,9}
----> 2 var_set.add([10,11])
      3 print(var_set)

TypeError: unhashable type: 'list'
```

In \[21]:

```
var_set = {1,2,3,4,5,6,'console',7,8,9}
var_set.add({10,11})
print(var_set)
```

```
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-21-286db87b4ce1> in <module>
      1 var_set = {1,2,3,4,5,6,'console',7,8,9}
----> 2 var_set.add({10,11})
      3 print(var_set)

TypeError: unhashable type: 'set'
```

Though We are allowed to add immutable data types in sets like numbers , strings , tuples etc.

#### Adding iterables elements individually : union() and update() <a href="#adding-iterables-elements-individually-union-and-update" id="adding-iterables-elements-individually-union-and-update"></a>

#### union(): <a href="#union" id="union"></a>

union() method adds elements of an iterables individually in a set. It returns a set with added elements . For Example:

In \[2]:

```
set_a = {1,2,3,4,5}
set_b = {6,7,8,9}
newset = set_a.union(set_b)
print(newset)
```

```
{1, 2, 3, 4, 5, 6, 7, 8, 9}
```

In \[3]:

```
set_a = {1,2,3,4,5}
list_b = [6,7,8,9]
newset = set_a.union(list_b)
print(newset)
```

```
{1, 2, 3, 4, 5, 6, 7, 8, 9}
```

Hence , You can add elements of any iterable in set.

#### update(): <a href="#update" id="update"></a>

update() method adds elements of an iterables individually in a set just like union.The only difference is it does not return any value and adds element in First set . For Example:

In \[4]:

```
set_a = {1,2,3,4,5}
set_b = {6,7,8,9}
set_a.update(set_b)
print(set_a)
```

```
{1, 2, 3, 4, 5, 6, 7, 8, 9}
```

If i want to change set\_b , i will write above code something like this.

In \[6]:

```
set_a = {1,2,3,4,5}
set_b = {6,7,8,9}
set_b.update(set_a)
print(set_b)
```

```
{1, 2, 3, 4, 5, 6, 7, 8, 9}
```

#### How to remove set items from set using methods : remove() , discard() , pop() <a href="#how-to-remove-set-items-from-set-using-methods-remove-discard-pop" id="how-to-remove-set-items-from-set-using-methods-remove-discard-pop"></a>

#### remove(): <a href="#remove" id="remove"></a>

remove() method removes the element from set. It takes only one argument.

Parameter :

element : An element that we want to remove.

For Example:

In \[7]:

```
set_a = {1,2,3,4,5}
set_a.remove(5)
print(set_a)
```

**Note:**&#x72;emove method will throw an error if element to be removed does not exist in set.

In \[9]:

```
set_a = {1,2,3,4,5}
set_a.remove(7)  #7 does not exist in set
print(set_a)
```

```
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-9-778c40fc87bb> in <module>
      1 set_a = {1,2,3,4,5}
----> 2 set_a.remove(7)  #7 does not exist in set
      3 print(set_a)

KeyError: 7
```

#### discard(): <a href="#discard" id="discard"></a>

discard() method removes the element from set. It takes only one argument.

Parameter :

element : An element that we want to remove.

For Example:

In \[10]:

```
set_a = {1,2,3,4,5}
set_a.remove(5)
print(set_a)
```

#### Difference between remove() and discard(): <a href="#difference-between-remove-and-discard" id="difference-between-remove-and-discard"></a>

remove() and discard() works in same way. The only difference is remove throws an error if value to be removed does not exist in set , while discard does not throw any error. For Example:

In \[11]:

```
set_a = {1,2,3,4,5}
set_a.discard(7)  #7 does not exist in set
print(set_a)
```

#### pop(): <a href="#pop" id="pop"></a>

You can also use the pop() method to remove an item, but this method will remove a random item. Remember that sets are unordered, so you will not know what item that gets removed. It has no parameters.

The return value of the pop() method is the removed item.

In \[12]:

```
set_a = {1,2,3,4,5}
set_a.pop()
print(set_a)
```

It also returns the deleted value from set. For Example:

In \[13]:

```
set_a = {1,2,3,4,5}
item = set_a.pop()
print(set_a)
print("deleted item is",item)
```

```
{2, 3, 4, 5}
deleted item is 1
```

#### difference() and difference\_update(): <a href="#difference-and-difference_update" id="difference-and-difference_update"></a>

difference() method returns the uncommon values in the set. for example:

In \[14]:

```
set_a = {1,2,3,4,5,6}
set_b = {4,5,6,7,8,9}
difference_set = set_a.difference(set_b)  #uncommon values of set_a is returned.
print(difference_set)
```

In \[15]:

```
set_a = {1,2,3,4,5,6}
set_b = {4,5,6,7,8,9}
difference_set = set_b.difference(set_a)  #uncommon values of set_b is returned.
print(difference_set)
```

#### difference\_update : <a href="#difference_update" id="difference_update"></a>

difference\_update removes the items in this set that are also included in another, specified set.It does not return any value.

In \[16]:

```
set_a = {1,2,3,4,5,6}
set_b = {4,5,6,7,8,9}
set_a.difference_update(set_b)
print(set_a)
```

In \[18]:

```
set_a = {1,2,3,4,5,6}
set_b = {4,5,6,7,8,9}
set_b.difference_update(set_a)
print(set_b)
```

#### intersection() and intersection\_update(): <a href="#intersection-and-intersection_update" id="intersection-and-intersection_update"></a>

intersection() returns common values from two sets. For Example:

In \[19]:

```
set_a = {1,2,3,4,5,6}
set_b = {4,5,6,7,8,9}
common = set_a.intersection(set_b)
print(common)
```

#### intersection\_update(): <a href="#intersection_update" id="intersection_update"></a>

intersection\_update removes uncommon values from the set. It does not return any value . For example:

In \[20]:

```
set_a = {1,2,3,4,5,6}
set_b = {4,5,6,7,8,9}
set_a.intersection_update(set_b)
print(set_a)
```

#### symmetric\_difference and symmetric\_difference\_update: <a href="#symmetric_difference-and-symmetric_difference_update" id="symmetric_difference-and-symmetric_difference_update"></a>

#### symmetric\_difference: <a href="#symmetric_difference" id="symmetric_difference"></a>

symmetric\_difference method returns a set comprises of uncommon values from both sets. For Example:

In \[21]:

```
set_a = {1,2,3,4,5,6}
set_b = {4,5,6,7,8,9}
newset = set_a.symmetric_difference(set_b)
print(newset)
```

#### symmetric\_difference\_update : <a href="#symmetric_difference_update" id="symmetric_difference_update"></a>

This method changes the value of first set. where values are uncommon values from both sets. For example:

In \[22]:

```
set_a = {1,2,3,4,5,6}
set_b = {4,5,6,7,8,9}
set_a.symmetric_difference_update(set_b)
print(set_a)
```

#### issubset: <a href="#issubset" id="issubset"></a>

subset means if all the elements of set A is present in set B. Set A is a subset of B.

issubset() method returns true if Set A is subset of Set B.

In \[23]:

```
set_b = {1,2,3,4,5,6}
set_a = {4,5,6}
sub = set_a.issubset(set_b)
print(sub)
```

#### issuperset: <a href="#issuperset" id="issuperset"></a>

superset means if all the elements of set A is present in set B. set B is superset of set A.

issuperset() method returns true if Set B is superset of Set A. For Example:

In \[24]:

```
set_b = {1,2,3,4,5,6}
set_a = {4,5,6}
sup = set_b.issuperset(set_a)
print(sup)
```

#### isdisjoint() : <a href="#isdisjoint" id="isdisjoint"></a>

Two sets are disjoint when there is no common value between two sets. It returns True if no values are common in sets otherwise False.

In \[25]:

```
set_b = {1,2,3,4,5,6}
set_a = {7,8,9}
output = set_a.isdisjoint(set_b)
print(output)
```

In \[26]:

```
set_b = {1,2,3,4,5,6}
set_a = {1,7,8,9}
output = set_a.isdisjoint(set_b)
print(output)
```

#### clear(): <a href="#clear" id="clear"></a>

To clear all the contents of set , we use clear() method.

In \[27]:

```
set_b = {1,2,3,4,5,6}
set_b.clear()
print(set_b)
```

#### copy() : <a href="#copy" id="copy"></a>

To copy all the contents of a set in another set, we use copy method. For Example:

In \[28]:

```
set_a = {1,2,3,4,5,6}
newset = set_a.copy()
print(newset)
```

#### set() Constructor : <a href="#set-constructor" id="set-constructor"></a>

set() constructor returns an iterable into set. For Example:

In \[29]:

```
name = "Console Flare"
name = set(name)
print(name)
```

```
{'C', 'o', 'F', 'l', 's', ' ', 'a', 'e', 'n', 'r'}
```

In \[30]:

```
name = [1,2,3]
name = set(name)
print(name)
```

#### How to create an Empty set: <a href="#how-to-create-an-empty-set" id="how-to-create-an-empty-set"></a>

To create an empty set , we cannot use curly braces{}. Because curly braces are used to signify empty dictionary.

To create an empty set , we will use set() constructor. For Example:

In \[31]:

```
empty_set = set()
print(empty_set)
```

```
set()
```
