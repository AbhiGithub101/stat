# 13. List

## 9.Lists In Python

### What is List?

A list can be defined as a collection of **values** or **items** of different Data types.

In more simpler terms, List is a collection of items enclosed between Square brackets \[]. Unlike other data types like Integer , Float and boolean, List stores multiple values in a single variable. For Example:

In \[1]:

```python
varlist = [1,2,3,4,5,6,7,8,9]
print(varlist)
```

```
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Memory Allocation of List items:

As we know that Lists are a sequence of items, hence Each item of list gets store in different memory block, something like this:

In \[ ]:

```
varlist = ["console","flare","python","data"]
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FOxSdlc9vR15eCq28I4PR%2Fimage.png?alt=media&#x26;token=6600aa92-cca4-4634-be37-d3c9c9bac2dd" alt=""><figcaption></figcaption></figure>

**You Must have realized that there are a lot of similarity in a string and list. We will cover that in detail in this session.**

### Indexing of Lists:

As we know that items of lists are stored in different memory blocks, each item within a list is given an index number.

Python offers two different indexing :

Positive Index Numbers : Positive index numbers starts from zero (0) and left to right.

Negative Index Numbers: Negative index numbers starts from -1 and from right to left.

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2F9T4JYJWOQhhh7iKzZYKI%2Fimage.png?alt=media&#x26;token=473b9fde-01c4-4ebe-a9ba-a9481956b1b6" alt=""><figcaption></figcaption></figure>

```
varlist = ["console","flare","python","data"]
varlist[1]
```

Out\[2]:

```
'flare'
```

In \[3]:

```
varlist = ["console","flare","python","data"]
varlist[-1]
```

Out\[3]:

```
'data'
```

### Slicing in lists:

Slicing in lists is done in same way as we do slicing in strings. For Example:

In \[4]:

```
varlist = ["console","flare","python","data"]
varlist[1:3]
```

Out\[4]:

```
['flare', 'python']
```

In \[6]:

```
varlist = ["console","flare","python","data"]
varlist[-2:]
```

Out\[6]:

```
['python', 'data']
```

### How to Create an empty list:

Empty list is a list with no items in it. We can create an empty list by using \[].

In \[28]:

```
empty_list = []
print(empty_list)
```

```
[]
```

### Properties of a list:

**1.Lists are Ordered:**

When You define a list , its items are stored and assigned to specific index number. It means list items are ordered . To Explain it better, Here is an Example:

```
varlist =["console","flare","python","data"]
print(varlist)
print(varlist)
print(varlist)
```

```
['console', 'flare', 'python', 'data']
['console', 'flare', 'python', 'data']
['console', 'flare', 'python', 'data']
```

**No matter , How many times you print list , items are assigned to their particular index number and won't change their place unless we do it deliberately.In \[ ]:**

To understand it even more better, Let's take two list with same data items and compare it.

```
varlist = ['console', 'flare', 'python', 'data']
anotherlist = ['console', 'flare', 'data', 'python']
compare = varlist == anotherlist
print(compare)
```

**Output : False**

Here items in varlist and anotherlist is same but both lists are in different order. Lists maintain the order of the element for the lifetime. It does not chnage its order unless we do it.

**1.Lists are Mutable/Changeable:**

We can change the items in list with the help of item assignment. For example:

```
varlist = ["console","flare","python","data"]
varlist[3]="Data Science"
print(varlist)
```

```
['console', 'flare', 'python', 'Data Science']
```

**It will throw us an error (index out of range) , if we try to assign values out of range.**

**In \[10]:**

```
varlist = ["console","flare","python","data"]
varlist[5]="Data Science"
print(varlist)
```

```python
IndexError                                Traceback (most recent call last)
<ipython-input-10-202c9277abcd> in <module>
      1 varlist = ["console","flare","python","data"]
----> 2 varlist[5]="Data Science"
      3 print(varlist)

IndexError: list assignment index out of range
```

**3.Lists allows duplicate values:**

List allows duplicate values, it can have as many duplicate values. For Example:

```python
varlist = ["console","flare","python","data","python","python"]
print(varlist)
```

```
['console', 'flare', 'python', 'data', 'python', 'python']
```

### Functions used in List :

Functions that we used in string , we will be using them in List too.

**len() function:**

len() function is used to count items in a List. For Example:

```
varlist = ["console","flare","python","data"]
len(varlist)
```

```
4
```

**max() function:**

max() function is used to return largest value or item in a List , For Example:

```
varlist = [23,45,12,76,83]
max(varlist)
```

```
83
```

```
varlist = ["python","console","data"]
print(min(varlist))
print(max(varlist))
```

```
console
python
```

To understand above code better, Imagine a dictionary, the first value in dictionary is minimum and last value is maximum. 'console' comes before 'python' in dictionary.

**max() and min() function does not work in mixed lists. Mixed lists mean A list with items of different category of data types.**

```
varlist = ["python","console","data",1,2,3]
print(min(varlist))
print(max(varlist))
```

```
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-17-a0d202e95e64> in <module>
      1 varlist = ["python","console","data",1,2,3]
----> 2 print(min(varlist))
      3 print(max(varlist))

TypeError: '<' not supported between instances of 'int' and 'str'
```

### Type of a list: <a href="#type-of-a-list" id="type-of-a-list"></a>

```
varlist = [1,2,3]
type(varlist)
```

```
list
```

### List Operations: <a href="#list-operations" id="list-operations"></a>

**how to Concatenate two lists** $$+$$**:**

```python
var_list = [1,2,3,4,5,6,7,8,9]
another_list = ['a','b','c','d']
combined_list = var_list + another_list
print(combined_list)
```

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 'a', 'b', 'c', 'd']
```

**Repetition of two lists** $$∗$$**:**

```
var_list = [1,2,3,4,5,6,7,8,9]
rep_list = var_list * 2
print(rep_list)
```

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

**Membership operator in list:**

```
var_list = [1,2,3,4,5,6,7,8,9]
present = 1 in var_list
print(present)
```

```
True
```

### Iteration in list: <a href="#iteration-in-list" id="iteration-in-list"></a>

for loop is used to iterate over the list items. For example:

```
var_list = [1,2,3,4,5,6,7,8,9]

for i in var_list:
    print(i)
```

```python
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

### Updating List items with the help of item assignment:

Lists are the most versatile data structures in Python since they are mutable, and their values can be updated by using the slice and assignment operator.n

```python
list = [1, 2, 3, 4, 5, 6]     
print(list)     
# It will assign value to the value to the second index   
list[2] = 10   
print(list)    
# Adding multiple-element   
list[1:3] = [89, 78]     
print(list) 
```

```python
[1, 2, 3, 4, 5, 6]
[1, 2, 10, 4, 5, 6]
[1, 89, 78, 4, 5, 6]
```

#### List Methods:

Functions that are specific to list are known as list methods. We will go through each method one by one.

#### 1.Adding elements to the list:

append() Python provides append() function which is used to add an element to the list. However, the append() function can only add value to the end of the list.

It does not return any value.

append() only takes one argument.

```
var_list = [1,2,3,4,5,6,7,8,9]
var_list.append(10) #it will add value at the end of the list , means at 9th index.
print(var_list)
```

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

If we append iterables(string, list,tuple,set,dictionary) in list. It will add iterables as whole at the end of the list. For Example:

```
var_list = [1,2,3,4,5,6,7,8,9]
var_list.append([10,11,12])
print(var_list)
```

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, [10, 11, 12]]
```

```
var_list = [1,2,3,4,5,6,7,8,9]
var_list.append("python")
print(var_list)
```

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 'python']
```

### How to populate a list with user input values: <a href="#how-to-populate-a-list-with-user-input-values" id="how-to-populate-a-list-with-user-input-values"></a>

```
var_list = [] #empty list

for i in range(5):
    user_value = input(f"enter value for {i} index: ")
    var_list.append(user_value)

print("List : ",var_list)
```

```
enter value for 0 index: 1
enter value for 1 index: 2
enter value for 2 index: 3
enter value for 3 index: 4
enter value for 4 index: 5
List :  ['1', '2', '3', '4', '5']
```

### 2. extend() method:

The extend() method adds all the elements of an iterable (string,list, tuple, string,set) to the end of the list. extend() takes only one argument.For example:

```
var_list = [1,2,3,4,5,6,7,8,9]
var_list.extend([10,11,12])
print(var_list)
```

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
```

So, Here extend adds elements of iterable individually in the list.

```
var_list = [1,2,3,4,5,6,7,8,9]
var_list.extend("python")  #string is an iterable.
print(var_list)
```

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 'p', 'y', 't', 'h', 'o', 'n']
```

**Note:** append() and extend() adds element at the end of the list.

### How to add element at a specified index: insert()

insert() method adds an element at a specified index. It also has an argument.

Syntax: list.insert(index, element)

```
var_list = [1,2,3,4,5,6,7,8,9]
var_list.insert(5,10)  #inserts element 10 at 5th index
print(var_list)
```

```
[1, 2, 3, 4, 5, 10, 6, 7, 8, 9]
```

```
var_list = [1,2,3,4,5,6,7,8,9]
var_list.insert(5,[10,11,12])  #inserts element  at 5th index
print(var_list)
```

```
[1, 2, 3, 4, 5, [10, 11, 12], 6, 7, 8, 9]
```

### How to add a list or any other iterable to another list? <a href="#how-to-add-a-list-or-any-other-iterable-to-another-list" id="how-to-add-a-list-or-any-other-iterable-to-another-list"></a>

```
list_a = [1,2,3,4]
list_b = [5,6,7,8]
list_a.extend(list_b)
print(list_a)
```

```
[1, 2, 3, 4, 5, 6, 7, 8]
```

### Removing List Items:

As far we've learned How to add elements and iterables through various methods. There are methods that remove elements like pop and remove .

### remove() method :

remove() method removes the element from the list. It has one argument. It does not return any value.

syntax: **list.remove(value)**

```
varlist = ["console","flare","python","data"]
varlist.remove("data")
print(varlist)
```

```
['console', 'flare', 'python']
```

**Note:** remove() method will return error if value we want to remove does not exist in list.

```
varlist = ["console","flare","python","data"]
varlist.remove("PYTHON")
print(varlist)
```

```python
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-6-c24ea32b87ce> in <module>
      1 varlist = ["console","flare","python","data"]
----> 2 varlist.remove("PYTHON")
      3 print(varlist)

ValueError: list.remove(x): x not in list
```

### pop() method :

pop() method removes the element of a specified position or index.

pop() method returns the removed value also.

syntax: **list.pop(index)**

```
varlist = ["console","flare","python","data"]
varlist.pop(2)
print(varlist)
```

```
['console', 'flare', 'data']
```

**pop() method returns the removed value also.**

```
varlist = ["console","flare","python","data"]
item = varlist.pop(2)
print(varlist)
print("deleted item: ", item)
```

```
['console', 'flare', 'data']
deleted item:  python
```

**Note:**&#x70;op() method will return error if value we want to pop out does not exist in list.

### Clear all the elements in a list - clear():

To clear all the elements in a list, we use clear method. It has no argument and does not return any values.

```
varlist = ["console","flare","python","data"]
varlist.clear()
print(varlist)
```

```
[]
```

### copy elements of a list - copy():

To copy all the elements of a list in a list, we use copy method. It has no argument and does not return values.

```
varlist = ["console","flare","python","data"]
copylist = varlist.copy()
print(copylist)
```

```
['console', 'flare', 'python', 'data']
```

### To Reverse elements of a list - reverse():

To reverse all the elements of a list, we use reverse method. It has no argument and does not return values.

syntax: list.reverse()

```
varlist = ["console","flare","python","data"]
varlist.reverse()
print(varlist)
```

```
['data', 'python', 'flare', 'console']
```

### To sort the elements in a list - sort() :

To sort the elements of a list alphabetically or numerically we use sort()method. It does not return any value.

**Parameter:**

**reverse: Optional.** (reverse=True) will sort the list descending. Default is reverse=False

```
varlist = ["console","flare","python","data"]
varlist.sort()  #sort list items alphabetically in ascending order
print(varlist)
```

```
varlist = [45,36,78,21,1]
varlist.sort()  #sort list items numerically in ascending order
print(varlist)
```

```
[1, 21, 36, 45, 78]
```

We can also reverse the sorted list to show list items in descending order.

```
varlist = [45,36,78,21,1]
varlist.sort(reverse = True)  #sort list items numerically/alphabetically in descending order
print(varlist)
```

```
[78, 45, 36, 21, 1]
```

**Note:**&#x73;ort() will throw error for mixed list (list elements with different category of data types).

```
varlist = [45,36,78,21,1,'python']
varlist.sort()  
print(varlist)
```

```
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-11-9b35c607c747> in <module>
      1 varlist = [45,36,78,21,1,'python']
----> 2 varlist.sort()
      3 print(varlist)

TypeError: '<' not supported between instances of 'str' and 'int'
```

These were all the methods that we are going to use in a list.

### Deleting a list: del()

We can delete a list by using function del(). For example:

```
varlist = ["console","flare","python","data"]
del(varlist)
```

Now this list has been deleted , to show this better why don't we try to print list?

```
print(varlist)
```

```
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-3-c07dcacb9080> in <module>
----> 1 print(varlist)

NameError: name 'varlist' is not defined
```

### List Constructor - list():

List Constructor is used to convert an iterable(string,set,tuple,dictionary) into list. It has only one Parameter.

Syntax : list(iterable)

```
thistuple = (1,2,3)
thislist = list(thistuple)
print(thislist)
```

```
[1, 2, 3]
```

```
name = "ConsoleFlare"
namelist = list(name)
print(namelist)
```

```
['C', 'o', 'n', 's', 'o', 'l', 'e', 'F', 'l', 'a', 'r', 'e']
```

list() can also be used to create an empty list. For Example:

```
empty_list = list()
print(empty_list)
```

### List Comprehension:

List comprehension offers a shorter syntax when you want to create a new list based on the values of an existing list.

Syntax = \[expression for item in collection]

Example:

Based on a list of natural numbers , make a list of even numbers only. What should be the code?

```
natural_num = [1,2,3,4,5,6,7,8,8,8,9,10]

even_num = []

for i in natural_num:
    if(i%2==0):
        even_num.append(i)

print(even_num)
```

```
[2, 4, 6, 8, 8, 8, 10]
```

With the help of list Comprehension, You can write a single line of code to achieve the result.

```
natural_num = [1,2,3,4,5,6,7,8,8,8,9,10]

even_num = [i for i in natural_num if(i%2==0)] 

print(even_num)
```

```
[2, 4, 6, 8, 8, 8, 10]
```

**Note:**&#x49;t is not necessary to create a list from 'another list'. You can create a list even with other iterables , range etc.

### Multidimensional Lists in Python:

List can also contain lists as item within them. These are called **Nested Lists** or **Multidimensional lists.**

For Example:

```
multi_dim = [[1,2,3],[4,5,6],[7,8,9]]
print(multi_dim)
```

```
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

As You can see, multi\_dim is a Multidimensional list. It contains 3 list items in a list.

### Matrices and Multidimensional Lists:

You all have read Matrix in Mathematics.

Multidimensional list is treated as Matrix in Python. So before deep diving into Multidimensional List, Let's have a glance at matrix.

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FN10YLNAs0FH7zs3P09Qh%2Fimage.png?alt=media&#x26;token=d4c9b7f7-cd30-4808-b877-e3768713366f" alt=""><figcaption></figcaption></figure>

#### Dimension of Matrix or Multidimensional List:

Above figure has 2 Rows and 3 Columns. So the Dimension of this multidimensional list is 2 ∗ 3.

Above Matrix can be written in Python like:

```
multi_dim = [[6,4,24],[1,-9,8]]
print(multi_dim)
```

```
[[6, 4, 24], [1, -9, 8]]
```

We can also format it in matrix form like:

```
multi_dim = [  [6,4,24],
               [1,-9,8]
                        ]
print(multi_dim)
```

```
[[6, 4, 24], [1, -9, 8]]
```

### Indexing of Multidimensional List: <a href="#indexing-of-multidimensional-list" id="indexing-of-multidimensional-list"></a>

```
# Accesing a list  from mutli_dim list
multi_dim = [  [6,4,24],
               [1,-9,8]
                        ]
print(multi_dim[0])
```

```
[6, 4, 24]
```

```
# Accesing a list item from lists of mutli_dim list
multi_dim = [  [6,4,24],
               [1,-9,8]
                        ]
print(multi_dim[0][0])
```

```
6
```

```
multi_dim[0] = [6,4,24]
multi_dim[0][0] = 6
multi_dim[0][1] = 4
multi_dim[0][2] = 24
multi_dim[1][0] = 1
multi_dim[1][1] = -9
multi_dim[1][2] = 8
```

### To Create a MultiDimesional List from user input:

To Create a MultiDimensional List in Python , what we need first is Row and Column of multidimensional list.

```
row = int(input("Enter Row:"))
col = int(input("Enter Column:"))
```

```
Enter Row:2
Enter Column:3
```

Now we will need an empty list, so that we can populate it later with user values.

```
multi_dim = []
```

Now we need to iterate through rows and columns of list:

```
for i in range(row):
    listitem = []
    for j in range(col):
        user_value = input(f"Enter Value for {i} row and {j} column : ")
        listitem.append(user_value)
    multi_dim.append(listitem)

print("MultiDimensional list : ",multi_dim)
```

```
Enter Value for 0 row and 0 column : 6
Enter Value for 0 row and 1 column : 4
Enter Value for 0 row and 2 column : 24
Enter Value for 1 row and 0 column : 1
Enter Value for 1 row and 1 column : -9
Enter Value for 1 row and 2 column : 8
MultiDimensional list :  [['6', '4', '24'], ['1', '-9', '8']]
```

Now we need to represent this multidimensional list in matrix Form:

```
for i in multi_dim:
    print(i)
```

```
['6', '4', '24']
['1', '-9', '8']
```

```
Another way to represent Multidimensional List in Matrix Form :
```

```
for i in range(row):
    for j in range(col):
        print(multi_dim[i][j],end=" ")
    print()
```

```
6 4 24 
1 -9 8 
```

### Transpose of a Matrix:

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FnQidKinphlKWGH2YL6be%2Fimage.png?alt=media&#x26;token=fbcdb254-262a-4952-8f15-848d21a8c609" alt=""><figcaption></figcaption></figure>

"Flipping" a matrix over its diagonal. The rows and columns get swapped.

Example: the value in the 1st row and 3rd column ends up in the 3rd row and 1st column.

```
multi_dim = [ [6,4,24],
              [1,-9,8]
                      ]
row = len(multi_dim)
col = len(multi_dim[0])

print("-------Original Matrix--------")
for i in multi_dim:
    print(i)
```

```
-------Original Matrix--------
[6, 4, 24]
[1, -9, 8]
```

Now as we know, To transpose a matrix

1.first thing that we need to do, is to swap the row and column of the original matrix.

2.Second thing is to Create a Zero matrix of same Dimension.

```
T = []
rowT = col
colT = row

for i in range(rowT):
    listitem = []
    for j in range(colT):
        listitem.append(0)
    T.append(listitem)

for i in T:
    print(i)
```

```
[0, 0]
[0, 0]
[0, 0]
```

Now to update values :

```
for i in range(rowT):
    for j in range(colT):
        T[i][j]=multi_dim[j][i]

for i in T:
    print(i)
```

```
[6, 1]
[4, -9]
[24, 8]
```

This is the Transpose of the Matrix multi\_dim.

### Addition of Two Matrices: <a href="#addition-of-two-matrices" id="addition-of-two-matrices"></a>

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2Fgu2jfv6Fu7HiXK45aNP7%2Fimage.png?alt=media&#x26;token=0ec1dc1a-ea37-4a69-b684-518c9166725b" alt=""><figcaption></figcaption></figure>

The two matrices must be the same size,the rows must match in size, and the columns must match in size.

Example: a matrix with 3 rows and 5 columns can only be added to another matrix of 3 rows and 5 columns.

```
matrix_a = [[3,8],
            [4,6]
                  ]

matrix_b = [[4,0],
            [1,-9]
                  ]

add_matrix = [[0,0],
               [0,0]
                    ]
row = len(matrix_a)
col = len(matrix_a[0])

for i in range(row):
    for j in range(col):
        add_matrix[i][j]= matrix_a[i][j]+matrix_b[i][j]

for i in add_matrix:
    print(i)
```

```
[7, 8]
[5, -3]
```

### Multiplication of Two Matrices:

To multiply a matrix by another matrix we need to do the "dot product" of rows and columns ... what does that mean? Let us see with an example:

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2Fc4QLasc8TzlXLUstTQBU%2Fimage.png?alt=media&#x26;token=df1c3003-604b-43e3-9e2b-cf39bd98de5d" alt=""><figcaption></figcaption></figure>

As You have noticed Multiplying 2$$∗$$∗3 Matrix with 3$$∗$$∗2 Matrix , gives us 2$$∗$$∗2 Matrix.

It means multiplying a list with dimension X _Y with a list of dimension Y_ Z will result in a matrix of X \* Z.

When we do Multiplication:

1.The number of columns of the 1st matrix must equal the number of rows of the 2nd matrix.\\

2.And the result will have the same number of rows as the 1st matrix, and the same number of columns as the 2nd matrix.

```
# Program to multiply two matrices using nested loops

# 3x3 matrix
X = [[12,7,3],
    [4 ,5,6],
    [7 ,8,9]]
# 3x4 matrix
Y = [[5,8,1,2],
    [6,7,3,0],
    [4,5,9,1]]
# result is 3x4
result = [[0,0,0,0],
         [0,0,0,0],
         [0,0,0,0]]

# iterate through rows of X
for i in range(len(X)):
   # iterate through columns of Y
   for j in range(len(Y[0])):
       # iterate through rows of Y
       for k in range(len(Y)):
           result[i][j] += X[i][k] * Y[k][j]

for r in result:
   print(r)
```

```
[114, 160, 60, 27]
[74, 97, 73, 14]
[119, 157, 112, 23]
```

### Assignment :

1.Take 10 integer inputs from user and store them in a list and print them on screen.\
\
2.Take 20 integer inputs from user and print the following:\
\
number of positive numbers\
number of negative numbers\
number of odd numbers\
number of even numbers\
number of 0s.\
\
3.Write a program to print sum, average of all numbers, smallest and largest element of a list.\
\
4.Make a list by taking 10 input from user. Now delete all repeated elements of the list.\
E.g.-\
\
INPUT : \[1,2,3,2,1,3,12,12,32]\
OUTPUT : \[1,2,3,12,32]\
\
5.Take a list of length n where all the numbers are non-negative and unique. Find the element in the list possessing the highest value. Split the element into two parts where first part contains the next highest value in the list and second part hold the required additive entity to get the highest value. Print the list where the highest value get splitted into those two parts.\
\
Sample input: 4 8 6 3 2\
Sample output: 4 6 2 6 3 2\
\
6.Write a program to add and multiply two 3x3 matrices.
