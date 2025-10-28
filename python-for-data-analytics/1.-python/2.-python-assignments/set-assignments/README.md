# Set Assignments

1. Write a python program to remove duplicate from a list using set.

<details>

<summary>Solution</summary>

```python
lst = [2, 3, 4, 2, 5, 4, 3, 7]
print(f'Original List : {lst}')
lst = list(set(lst))
print(f'New List : {lst}')
```

</details>

2. Write a program to carry out the following operations on the given set\
   s = {10, 2, -3, 4, 5, 88}\
   1\. number of items in set s\
   2\. maximum element in set s\
   3\. minimum element in set s\
   4\. sum of all elements in set s\
   5\. obtain a new sorted set from s, set s remaining unchanged\
   6\. report whether 100 is an element of s\
   7\. report whether -3 is an element of s

<details>

<summary>Solution</summary>

```python
s= {10, 2, -3, 4, 5, 88}
print(len(s))
print(max(s))
print(min(s))
print(sum(s))
print(set(sorted(s)))
print(100 in s)
print(-3 in s)

```

</details>

3. A Set contains names which begins either with A or with B, write a program to separate out the names into two sets, one containing names beginning with A and another containing names beginning with B.

<details>

<summary>Solution</summary>

```python
s = {'aakrosh', 'aman', 'alok', 'benn', 'baahu'}
print(s)
set_a = set()
set_b = set()
for i in s:
    if i.lower().startswith('a'):
        set_a.add(i)
    elif i.lower().startswith('b'):
        set_b.add(i)

print(set_a)
print(set_b)

```

</details>

4. Create an empty set. Write a program that add five new names to this set, modifies one existing name and deletes two name existing in it.

<details>

<summary>Solution</summary>

```python
s = set()
for i in range(5):
    s.add(input('Enter Number : '))
print('Actual Set : ', s)
name = input('Enter name to modify : ')
if name in s:
    s.remove(name)
    mod_n = input('Enter the new name : ')
    s.add(mod_n)
else:
    print(name, 'Doesn\'t exist')
print('Modified Set : ', s)
#Now Deleting two names existing in the list
n1 = input('Enter Name 1 : ')
n2 = input('Enter Name 2 : ')
s.remove(n1)
s.remove(n2)
print('Modified Set : ', s)
```

</details>

5. Write a program to show the difference between the two set functions **discard() and remove().**

<details>

<summary>Solution</summary>

```python
s = {1, 2, 3, 4, 5}

s.remove(6) # error
s.discard(6) # no error 
#remove() gives error and discard() dont give error if value doesnt exist.
```

</details>

6. Write a program to create a set containing 10 randomly generated numbers in the range 15 to 45. Count how many of these numbers are less than 30. Delete all the numbers which are greater than 35.

<details>

<summary>Solution</summary>

```python
import random
s = {random.randrange(15, 45) for i in range(10)}
r = set()
print(s)
count = 0
for i in s:
    if i < 30:
        count += 1
    elif i > 35:
        r.add(i)

s = s.difference(r)
print(count)
print(s)

```

</details>

7. You are given a string remove the duplicates from that string using set.

<details>

<summary>Solution</summary>

```python
st = input('Enter String : ')
print(st)
s = set(st)
new_st = "".join(s)
print(new_st)
```

</details>

8. Write a python program to create a set using user input.

<details>

<summary>Solution</summary>

```python
s = set()
for i in range(5):
    val = int(input('Enter number : '))
    s.add(val)
```

</details>

9. Write a python program to iterate over set.

<details>

<summary>Solution</summary>

```python
#Assume the set s created in above question.
for i in s:
    print(i)
```

</details>

10. Take two sets and print the set after union of both the sets.(You can either create a set through random module and through user input).

<details>

<summary>Solution</summary>

```python
import random as rd
s1 = {rd.randrange(1, 100) for i in range(10)}
s2 = {rd.randrange(1, 100) for i in range(10)}

print(f's1 : {s1}')
print(f's2 : {s2}')
print(s1.union(s2))
```

</details>

11. Take two sets and print the set after intersection of both the sets.

<details>

<summary>Solution</summary>

```python
import random as rd
s1 = {rd.randrange(1, 100) for i in range(10)}
s2 = {rd.randrange(1, 100) for i in range(10)}
print(s1)
print(s2)
print(s1.intersection(s2))
```

</details>

12. Take two sets A and B and print the whether A is the subset of B.

<details>

<summary>Solution</summary>

```python
A = {1, 2, 3}
B = {1, 2, 3, 4, 5}

if A.issubset(B):
    print("A is a subset of B")
else:
    print("A is not a subset of B")

```

</details>

13. Take two sets A and B and print whether A is the superset of B or not.

<details>

<summary>Solution</summary>

```python
A = {1, 2, 3, 4, 5}
B = {1, 2, 3}

if A.issuperset(B):
    print("A is a superset of B")
else:
    print("A is not a superset of B")
```

</details>

14. Take a string from user and print the unique count of vowels in the string.

<details>

<summary>Solution</summary>

```python
st = input('Enter a string : ')
s = set(st.replace(' ', ''))
count = 0
for i in s:
    if i.lower() in 'aeiou':
        count += 1

print('String : ', st)
print('Unique Count of vowels in the string : ', count)
```

</details>

15. Write a Python program that takes two sets as input and prints the common elements between the two sets.

<details>

<summary>Solution</summary>

```python
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}

common_elements = set1.intersection(set2)
print('common elements : ',common_elements)

```

</details>

16. Write a Python program that takes two sets as input and prints the elements that are in the first set but not in the second set.

<details>

<summary>Solution</summary>

```python
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}

unique_elements = set1.difference(set2)
print(unique_elements)
```

</details>

17. You have a list of customers who have purchased products from your online store. You want to identify customers who have purchased from your store in the past month and customers who have not made any purchases in the past month. How can you use sets to accomplish this task?

<details>

<summary>Solution</summary>

```python
# Customer list for the past month
past_month_customers = {'John', 'Jane', 'Bob', 'Alice', 'Tom'}

# All customer list
all_customers = {'John', 'Jane', 'Bob', 'Alice', 'Tom', 'David', 'Sam'}

# Customers who have purchased in the past month
purchased_last_month = past_month_customers.intersection(all_customers)

# Customers who have not purchased in the past month
not_purchased_last_month = all_customers - purchased_last_month

print('Customers who have purchased in the past month:', purchased_last_month)
print('Customers who have not purchased in the past month:', not_purchased_last_month)

```

</details>

18. You are the owner of a restaurant and you want to identify the most popular menu items among your customers. You have a list of all menu items that have been ordered in the past month. How can you use sets to identify the most popular menu items?

<details>

<summary>Solution</summary>

```python
# Menu items ordered in the past month
past_month_menu_items = {'burger', 'fries', 'pizza', 'pasta', 'sandwich', 'salad', 'soup', 'steak'}

# All menu items
all_menu_items = {'burger', 'fries', 'pizza', 'pasta', 'sandwich', 'salad', 'soup', 'steak', 'chicken', 'fish', 'tacos', 'sushi'}

# Most popular menu items
most_popular_items = past_month_menu_items.intersection(all_menu_items)

print('Most popular menu items:', most_popular_items)
```

</details>

19. You are the manager of a retail store and you want to identify which products are selling well and which products are not. You have a list of all products sold in the past month. How can you use sets to identify the top selling products and the least selling products?

<details>

<summary>Solution</summary>

```python
# Products sold in the past month
past_month_products = {'shirt', 'pants', 'jacket', 'hat', 'shoes', 'sunglasses', 'purse', 'socks'}

# All products
all_products = {'shirt', 'pants', 'jacket', 'hat', 'shoes', 'sunglasses', 'purse', 'socks', 'gloves', 'scarf', 'belt', 'watch'}

# Top selling products
top_selling_products = {'shirt', 'pants', 'jacket', 'shoes'}

# Least selling products
least_selling_products = all_products - past_month_products

print('Top selling products:', top_selling_products)
print('Least selling products:', least_selling_products)
```

</details>

20. You are a data analyst and you want to identify the most common words used in a text document. You have a list of all words used in the document. How can you use sets to identify the most common words?

<details>

<summary>Solution</summary>

```python
# List of all words in the document
all_words = ['apple', 'banana', 'cherry', 'banana', 'apple', 'apple', 'cherry', 'date', 'cherry']

# Create a set of unique words in the document
unique_words = set(all_words)

# Initialize variables to store the most common word and its count
most_common_word = ''
most_common_count = 0

# Loop through each unique word and count its frequency in the document
for word in unique_words:
    count = all_words.count(word)
    # Check if the current word has a higher count than the most common word
    if count > most_common_count:
        most_common_word = word
        most_common_count = count

print('The most common word is:', most_common_word)
print('The count of the most common word is:', most_common_count)

```

</details>

21. You have a list of orders and their respective statuses (e.g. "pending", "shipped", "delivered"), and you want to count the number of orders in each status. How can you use sets to accomplish this task?

<details>

<summary>Solution</summary>

```python
# List of orders and their statuses
orders = [('Order 1', 'pending'), ('Order 2', 'shipped'), ('Order 3', 'delivered'),
          ('Order 4', 'pending'), ('Order 5', 'delivered'), ('Order 6', 'delivered')]

# Create sets of the different order statuses
pending = set([o[0] for o in orders if o[1] == 'pending'])
shipped = set([o[0] for o in orders if o[1] == 'shipped'])
delivered = set([o[0] for o in orders if o[1] == 'delivered'])

# Count the number of orders in each status
num_pending = len(pending)
num_shipped = len(shipped)
num_delivered = len(delivered)

print('Number of orders in pending status:', num_pending)
print('Number of orders in shipped status:', num_shipped)
print('Number of orders in delivered status:', num_delivered)

```

</details>
