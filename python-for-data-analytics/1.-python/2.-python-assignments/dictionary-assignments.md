# Dictionary Assignments

### Dictionary Creations

1.  Creat a dictionary using user input.\\

    ```
    employee_dict = { 
                     "John" : {"salary" : 5000, "department" : "Sales"},
                     "Mike" : {"salary" : 6000, "department" : "Marketing"},
                     "Sara" : {"salary" : 7000, "department" : "Operations"}
                     }
    ```

<details>

<summary>Solution:</summary>

```python
employee_dict={}

for i in range(3):
    name= input('Enter Name:')
    d1={}
    for i in range(1,3):
        key=input(f'Enter key no. {i}:')
        value=input(f'Enter value no. {i}:')
        d1[key]=value
        print()
    employee_dict[name]=d1

print(employee_dict)
```

</details>

2. Create a dictionary using user input.\
   employee\_dict={\
   'name' : \[ 'john' , 'mike' , 'sara'],\
   'salary' : \[ '5000' , '6000' , '7000'] ,\
   'department' : \['sales' , 'marketing' , 'operartions' ]\
   }

<details>

<summary>Solution</summary>

```python
employee_dict={}

for i in range(1,4):
    key= input(f'Enter key no. {i}:')
    l1=[]
    for i in range(1,4):
        value=input(f'Enter value no. {i} for {key}:')
        l1.append(value)
        print()
    employee_dict[key]=l1

print(employee_dict)
```

</details>

3. Create a dictionary where you have to take 3 inputs from the user and take keys from this list.\
   l1=\[ 'name' , 'salary' , 'department' ]\
   employee\_dict={\
   'name' : \[ 'john' , 'mike' , 'sara'],\
   'salary' : \[ '5000' , '6000' , '7000'] ,\
   'department' : \['sales' , 'marketing' , 'operartions' ]\
   }

<details>

<summary>Solution</summary>

```python
l1=[ 'name' , 'salary' , 'department' ]
employee_dict={}

for key in l1:    
    l2=[]
    for i in range(1,4):
        value=input(f'Enter value no. {i} for {key}:')
        l2.append(value)
        
    employee_dict[key]=l2
    print()

print(employee_dict)
```

</details>

4. Create a list of 4 dictionaries and each dictionary holds name, roll\_no, city, and stream of each student.\
   l1=\[\
   {'name' : 'ajay', 'roll\_no': '001', 'city' : 'pune', 'stream':'science' },\
   {'name' : 'anuj', 'roll\_no': '002', 'city' : 'mumbai', 'stream':'commerce' },\
   {'name' : 'anil', 'roll\_no': '003', 'city' : 'agra', 'stream':'arts' },\
   ]

<details>

<summary>Solution</summary>

```python
employee_dict= []

for i in range(3):
    dictionary = {}
    name = input(f'Enter name for student {i+1} :  ')
    roll_num = input(f'Enter roll no. for student {i+1} :  ')
    city = input(f'Enter city for student {i+1} :  ')
    stream = input(f'Enter stream for student {i+1} :  ')

    dictionary['name'] = name
    dictionary['roll_num'] = roll_num
    dictionary['city'] = city
    dictionary['stream'] = stream
    print(dictionary)
    employee_dict.append(dictionary)
    print()

print(employee_dict)
```

</details>

### Dictionary Operations

1. Create a dictionary called `fruit_dict` with the following **key-value** pairs: "apple" : 1, "banana" : 2, "orange" : 3. Also print fruit\_dict.

<details>

<summary>Solution</summary>

```python
fruit_dict = {'apple':1, 'banana':2, 'orange':3}
print(fruit_dict)
```

</details>

2. Write a program to add a fruit **mango** in the **fruit\_dict** and print all the fruit names.

<details>

<summary>Solution</summary>

```python
fruit_dict['mango'] = 4
print(fruit_dict)
for i in fruit_dict.keys():
    print(i)
```

</details>

3. Write a program to print the serial order of all the fruits in `fruit_dict.`

<details>

<summary>Solution</summary>

```python
for i in fruit_dict.values():
    print(i)
```

</details>

4. Write a program to create a dictionary which contains the `fruit name` and `their prices(float).` **Take fruit name and prices from user.** Create for 5 fruits.

<details>

<summary>Solution</summary>

```python
fruit = {}
for i in range(5):
    fruit[input('Enter Fruit Name : ')] = float(input('Enter Price : '))

print(fruit)

```

</details>

5. Write a program to count the frequency of each word in the given sentence: "the quick brown fox jumps over the lazy dog".

<details>

<summary>Solution</summary>

```python
sentence =input('Enter sentence : ')
word_list = sentence.split()
word_freq = {}
for word in word_list:
    if word in word_freq:
        word_freq[word] += 1
    else:
        word_freq[word] = 1
print(word_freq)
```

</details>

6. Create a dictionary `my_dict` with three key-value pairs: "name" : "John", "age" : 30, "city" : "New York".

* Write a program to check if the key "name" is in `my_dict`.
* Write a program to check if the value "Chicago" is in `my_dict`.
* Write a program to get the length of `my_dict`.
* Write a program to clear all the elements in `my_dict`.

<details>

<summary>Solution</summary>

```python
my_dict = {"name" : "John", "age" : 30, "city" : "New York"}

if "name" in my_dict:
    print("Key exists!")
else:
    print("Key does not exist.")

if "Chicago" in my_dict.values():
    print("Value exists!")
else:
    print("Value does not exist.")

print(len(my_dict))
my_dict.clear()
```

</details>

7. Create two dictionaries `dict1` and `dict2` with the following key-value pairs: "a" : 1, "b" : 2, "c" : 3 and "c" : 4, "d" : 5, "e" : 6 respectively.

* Write a program to merge `dict2` into `dict1`.
* Write a program to create a new dictionary that contains only the key-value pairs that are common in both `dict1` and `dict2`.
* Write a program to remove a key-value pair from `dict1`.

<details>

<summary>Solution</summary>

```python
dict1 = {'a':1, 'b':2, 'c':3}
dict2 = {'c':4, 'd':5, 'e':6}

print(dict1)
print(dict2)

dict1.update(dict2)
print(dict1)

common_dict = {k: dict1[k] for k in dict1 if k in dict2 and dict1[k] == dict2[k]}
print(common_dict)

dict1.pop('c')
print(dict1)
```

</details>

8. Write a program to sort a dictionary in ascending and descending both.\
   use d = {'oil':230, 'clip':150, 'stud':175, 'Nut':35}

<details>

<summary>Solution</summary>

```python
d = {'oil':230, 'clip':150, 'stud':175, 'Nut':35}
print(f'Original : {d}')

d1 = dict(sorted(d.items()))
print('Sorted In Ascending order : ', d1)
d2 = dict(sorted(d.items(), reverse=True))
print(f'Sorted in descending order : ', d2)
```

</details>

9. Write a program to check whether the dictionary is empty or not.

<details>

<summary>Solution</summary>

```python
d1 = {'Anil':45, 'Anmol':32}
if not d1:
    print('Dictionary is Empty')
```

</details>

10. Create a dictionary `employee_dict` with the following key-value pairs: "John" : {"salary" : 5000, "department" : "Sales"}, "Mike" : {"salary" : 6000, "department" : "Marketing"}, "Sara" : {"salary" : 7000, "department" : "Operations"}.

* Write a program to find the employee with the highest salary in `employee_dict`.
* Write a program to find the average salary of all employees in `employee_dict`.
* Write a program to add a new employee to `employee_dict`.
* Write a program to remove an employee from `employee_dict`.

<details>

<summary>Solution</summary>

```python
employee_dict = {"John" : {"salary" : 5000, "department" : "Sales"},
                 "Mike" : {"salary" : 6000, "department" : "Marketing"},
                 "Sara" : {"salary" : 7000, "department" : "Operations"}}

salary = []
max_sal = employee_dict['John']['salary']
for i in employee_dict.values():
    if i['salary']>max_sal:
        max_sal = i['salary']
    salary.append(i['salary'])    

for name, values in employee_dict.items():
    if values['salary'] == max_sal:
        print('Person with highest salary :', name)

average = sum(salary)/len(salary)
print('Average Salary :', average)

employee_dict["David"] = {"salary" : 8000, "department" : "Operations"}
del employee_dict["Mike"]
print(employee_dict)
```

</details>

11. Suppose you are working in a retail store and you want to keep track of sales by month. Write a program to create a dictionary `sales_dict` that stores the monthly sales data as follows:\
    \\

| Month | Sales |
| ----- | ----- |
| Jan   | 5000  |
| Feb   | 7000  |
| Mar   | 4500  |
| Apr   | 9000  |
| May   | 6000  |

\
Write a program to:

1. Print the sales in January.
2. Print the total sales for the first quarter (Jan to Mar).
3. Print the months in which sales were greater than 6000.
4. Add the sales data for June (8000) to the dictionary.
5. Remove the sales data for April from the dictionary.

<details>

<summary>Solution</summary>

```python
# Create the dictionary
sales_dict = {"Jan": 5000, "Feb": 7000, "Mar": 4500, "Apr": 9000, "May": 6000}

# 1. Print the sales in January.
print("Sales in January:", sales_dict["Jan"])

# 2. Print the total sales for the first quarter (Jan to Mar).
q1_sales = sales_dict["Jan"] + sales_dict["Feb"] + sales_dict["Mar"]
print("Total sales in Q1:", q1_sales)

# 3. Print the months in which sales were greater than 6000.
high_sales_months = [month for month, sales in sales_dict.items() if sales > 6000]
print("Months with sales greater than 6000:", high_sales_months)

# 4. Add the sales data for June (8000) to the dictionary.
sales_dict["Jun"] = 8000

# 5. Remove the sales data for April from the dictionary.
del sales_dict["Apr"]

```

</details>

12. You have been given the following data about the number of COVID-19 cases in different countries:\
    \
    cases{ "USA": 3500000, "India": 2300000, "Brazil": 1800000, "Russia": 1200000, "France": 800000, "UK": 700000, "Turkey": 650000, "Italy": 600000, "Spain": 550000, "Germany": 500000 }\
    \
    Write a program to find the top 3 countries with the highest number of COVID-19 cases.

<details>

<summary>Solution</summary>

```python
cases = {
    "USA": 3500000,
    "India": 2300000,
    "Brazil": 1800000,
    "Russia": 1200000,
    "France": 800000,
    "UK": 700000,
    "Turkey": 650000,
    "Italy": 600000,
    "Spain": 550000,
    "Germany": 500000
}

num_of_cases = sorted(list(cases.values()), reverse=True)[:3]

print("Top 3 countries with highest number of COVID-19 cases:")
for country, case in cases.items():
    if case in num_of_cases:
        print(f'{country} : {case}')        

```

</details>

13. You are given a dictionary `sales_data` containing sales information for a company's products. Each key-value pair in the dictionary represents a product's name and its corresponding sales in dollars for the year.\
    \
    sales\_data = { 'Product A': 15000, 'Product B': 25000, 'Product C': 30000, 'Product D': 40000, 'Product E': 50000 }
14. Write a program to calculate the total sales for the company.
15. Write a program to calculate the average sales per product.
16. Write a program to find the best-selling product.

<details>

<summary>Solution</summary>

```python
total_sales = sum(sales_data.values())
print(f"The total sales for the company is ${total_sales}.")

average_sales = total_sales / len(sales_data)
print(f"The average sales per product is ${average_sales:.2f}.")

best_selling_product = max(sales_data, key=sales_data.get)
print(f"The best-selling product is {best_selling_product}.")
```

</details>
