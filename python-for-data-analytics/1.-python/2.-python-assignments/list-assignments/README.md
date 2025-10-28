# List Assignments

### Basic Level Questions

1. Write a Python program that asks the user to enter a sentence and then prints the words in the sentence in alphabetical order.

<details>

<summary>Solution</summary>

```python
sentence = input("Enter a sentence: ")
words = sentence.split()
words.sort()
print("Words in alphabetical order:", " ".join(words))

#Python's default sorting order, uppercase letters are sorted before lowercase letters
```

</details>

2. Take name of five fruit from user through loop and store into a bucket made by list and print name of each fruit in the bucket.

<details>

<summary>Solution</summary>

```python
fruit_bucket = []
for i in range(5):
    fruit = input(f'Enter fruit {i+1} : ')
    fruit_bucket.append(fruit)
print()
print('Fruit Name')
for item in fruit_bucket:
    print(item)

```

</details>

3. Create a list of ten numbers and print only the even numbers in the list.

<details>

<summary>Solution</summary>

```python
num_list = []
for i in range(10):
    num = int(input(f'Enter Number {i+1} : '))
    num_list.append(num)
    
print('List Of Even Numbers : ',end=' ')
for i in num_list:
    if i % 2 == 0:
        print(i, end=' ')
```

</details>

4. Create a list of five strings and print the length of each string.

<details>

<summary>Solution</summary>

```python
my_list = ["apple", "banana", "cherry", "date", "elderberry"]
for item in my_list:
    print(len(item))
# Even User input can be taken as taken in above examples
```

</details>

5. Take a sentence from user and print only those words which are of even length.

<details>

<summary>Solution</summary>

```python
lis = input('Enter the sentence with spaces only : ').split()
print('Words of even length only')
for i in lis:
    if len(i) % 2 == 0:
        print(i)
```

</details>

6. Create a list of ten numbers and print the largest number in the list.

<details>

<summary>Solution</summary>

```python
my_list = [2, 7, 10, 13, 18, 23, 26, 31, 34, 39]
largest_num = my_list[0]
for num in my_list:
    if num > largest_num:
        largest_num = num
print(largest_num)

```

</details>

7. Write a python program to remove duplicates from a list.

<details>

<summary>Solution</summary>

```python
my_list = [1, 2, 2, 3, 4, 4, 5]
new_list = []
for i in my_list:
    if i not in new_list:
        new_list.append(i)
print(new_list)

```

</details>

8. Write a program to add all the elements of the list. Also find the length of the list using loop.

<details>

<summary>Solution</summary>

```
my_list = [131, 452, 673, 894, 523]
sum = 0
count = 0
for i in my_list:
    count += 1
    sum += i
print(sum)
print(count)

```

</details>

### Intermediate and Advanced Level Questions

9. Given a list of integers, write a program to find the sum of all even numbers in the list.\
   **Example**\
   **input**: `[1, 2, 3, 4, 5, 6]`\
   **Output:** `12`

<details>

<summary>Solution</summary>

```python
nums = [11, 22, 53, 84, 95, 106]
sum = 0
for num in nums:
    if num % 2 == 0:
        sum += num
print(sum)

```

</details>

10. Write a program to merge two lists into a single list without using the built-in `extend()` or `+` operators.\
    **Example**\
    **input:** `[1, 2, 3]`, `[4, 5, 6]`\
    **Output:** `[1, 2, 3, 4, 5, 6]`

<details>

<summary>Solution</summary>

```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]
for num in list2:
    list1.append(num)
print(list1)
#One might take the input from the user as well
```

</details>

11. Given a list of strings, write a program to find the longest string in the list.\
    **Example**\
    **input:** `['hello', 'world', 'how', 'are', 'you']`\
    **Output:** `'world'`

<details>

<summary>Solution</summary>

```python
strings = ['hello', 'world', 'how', 'are', 'you']
longest = ''
for string in strings:
    if len(string) > len(longest):
        longest = string
print(longest)
#One might take input from user as well
```

</details>

12. Reverse a list without using reverse() function.

<details>

<summary>Solution</summary>

```python
lis = [int(input('Enter Number : ')) for i in range(5)]
rev_lis = []
print(lis)
for i in range(len(lis)):
    rev_lis.append(lis[-(i+1)])
print(rev_lis)
```

</details>

13. Write a python program to find the common elements between two lists.

<details>

<summary>Solution</summary>

```python
#uses list comprehensions
lis1 = [int(input('Enter Number for list 1 : ')) for i in range(5)]
lis2 = [int(input('Enter Number for list 2 : ')) for i in range(5)]



for i in lis1:
    if i in lis2:
        print(i, end=' ')

```

</details>

14. Write a python program to create a list of numbers. Print the sum of the elements of even index and odd index separately.

<details>

<summary>Solution</summary>

```python
num_lis = []
#creating a list of 5 numbers
for i in range(5):
    num = int(input('Enter the number : '))
    num_lis.append(num)
#Now getting the sum of even index and odd index separately
even_sum = 0
odd_sum = 0
for i in range(5):
    if i % 2 == 0:
        even_sum += num_lis[i]
    else:
        odd_sum += num_lis[i]
        
print('Actual List : ', num_lis)
print('Even Index Elements sum : ', even_sum)
print('Odd Index Elements sum : ', odd_sum)

```

</details>

15. Write a program to store average marks of 10 students in a list and print the number of students falling the following categories in two columns:\
    \
    **Average Marks Number of Students**\
    1 - 30 xx\
    31 - 50 xx\
    51 - 70 xx\
    71 - 85 xx\
    86 - 100 xx

<details>

<summary>Solution</summary>

```python
avg_marks = [int(input('Enter Average Marks : ')) for i in range(10)]

#Initializing variables
cond1 = 0
cond2 = 0
cond3 = 0
cond4 = 0
cond5 = 0

for marks in avg_marks:
    if marks >= 1 and marks <= 30:
        cond1 += 1
    elif marks >= 31 and marks <= 50:
        cond2 += 1
    elif marks >= 51 and marks <= 70:
        cond3 += 1
    elif marks >= 71 and marks <= 85:
        cond4 += 1
    elif marks >= 86 and marks <= 100:
        cond5 += 1
    elif marks > 100:
        print('Marks not considerable')

print('\tAverage Marks\t\tNumber of students')
print(f'\t1 - 30\t\t\t{cond1}')
print(f'\t31 - 50\t\t\t{cond2}')
print(f'\t51 - 70\t\t\t{cond3}')
print(f'\t71 - 85\t\t\t{cond4}')
print(f'\t86 - 100\t\t\t{cond5}')

```

</details>

16. Write a program to create a list of numbers and print the list of numbers after reversing each number in the list.

<details>

<summary>Solution</summary>

```python
num_lis = []
rev_num_lis = []
for i in range(5):
    num = int(input('Enter the number : '))
    num_lis.append(num)

print('Original list: ', num_lis)
print('List after reversing each number: ')
for num in num_lis:
    reversed_num = 0
    while num > 0:
        remainder = num % 10
        reversed_num = (reversed_num * 10) + remainder
        num = num // 10
    rev_num_lis.append(reversed_num)
print('Reversed Number List : ', rev_num_lis)
```

</details>

17. Write a python program to create a list and sort it using the built-in function of list in descending order.

<details>

<summary>Solution</summary>

```python
num_lis = []
for i in range(5):
    num = int(input('Enter the number : '))
    num_lis.append(num)

num_lis.sort(reverse=True)
print('List after sorting in descending order: ', num_lis)
```

</details>

18. Write a program to create two lists of 5 numbers each and print the list after adding corresponding elements of the two lists.

<details>

<summary>Solution</summary>

```python
list1 = []
list2 = []

print('Enter elements of list1: ')
for i in range(5):
    num = int(input())
    list1.append(num)

print('Enter elements of list2: ')
for i in range(5):
    num = int(input())
    list2.append(num)

new_lis = []
for i in range(5):
    new_lis.append(list1[i] + list2[i])

print('List after adding corresponding elements of list1 and list2: ', new_lis)
```

</details>

19. Write a program to create a list of 5 numbers and print the list after replacing all the odd numbers with their squares.

<details>

<summary>Solution</summary>

```python
num_lis = []
for i in range(5):
    num = int(input('Enter the number : '))
    num_lis.append(num)

for i in range(5):
    if num_lis[i] % 2 != 0:
        num_lis[i] = num_lis[i] ** 2

print('List after replacing all the odd numbers with their squares: ', num_lis)
```

</details>

20. Write a program to create a list of 5 strings and print the list after reversing each string in the list.

<details>

<summary>Solution</summary>

```python
str_lis = []
for i in range(5):
    string = input('Enter the string : ')
    str_lis.append(string)

new_lis = []
for string in str_lis:
    new_lis.append(string[::-1])

print('List after reversing each string: ', new_lis)

```

</details>

21. Write a program to create a list of 5 strings and print the list after removing all the vowels from each string.

<details>

<summary>Solution</summary>

```python
str_lis = []
for i in range(5):
    string = input('Enter the string : ')
    str_lis.append(string)

new_lis = []
for string in str_lis:
    new_str = ''
    for char in string:
        if char.lower() not in 'aeiou':
            new_str += char
    new_lis.append(new_str)

print('List after removing all the vowels from each string: ', new_lis)
```

</details>

22. Write a program to create a list of 5 numbers and print the list after inserting a new number at the beginning of the list and sorting the list in ascending order.

<details>

<summary>Solution</summary>

```python
num_lis = []
for i in range(5):
    num = int(input('Enter the number : '))
    num_lis.append(num)

new_num = int(input('Enter the new number to insert at the beginning of the list: '))
num_lis.insert(0, new_num)
num_lis.sort()

print('List after inserting a new number at the beginning and sorting in ascending order: ', num_lis)
```

</details>

23. Take a sentence from user and print each word separated by ,

<details>

<summary>Solution</summary>

```python
sentence = input("Enter a sentence: ")   # take input from user
words = sentence.split()                 # split sentence into words
result = ", ".join(words)                # join words with comma separator
print(result)                            # print result
```

</details>

24. Write a program to create a list of 10 numbers and print the list after replacing each number with the difference between itself and the previous number in the list. The first number should remain the same.

<details>

<summary>Solution</summary>

```python
num_lis = [2, 5, 9, 15, 23, 33, 45, 59, 75, 93]
new_lis = [num_lis[0]]

for i in range(1, 10):
    new_lis.append(num_lis[i] - num_lis[i-1])

print('List after replacing each number with the difference between itself and the previous number: ', new_lis)
```

</details>

25. Write a program to create a list of 5 strings and print the list after removing all the strings which have a length less than the average length of all the strings in the list.

<details>

<summary>Solution</summary>

```python
str_lis = ['apple', 'banana', 'cherry', 'date', 'elderberry']
avg_len = sum(len(string) for string in str_lis) / len(str_lis)

new_lis = []
for string in str_lis:
    if len(string) >= avg_len:
        new_lis.append(string)

print('List after removing all the strings with length less than the average length: ', new_lis)
```

</details>

26. Write a program to create a list of 5 strings and print the list after removing all the vowels from the first and last strings in the list.

<details>

<summary>Solution</summary>

```python
str_lis = ['apple', 'banana', 'cherry', 'date', 'elderberry']

new_lis = []
for i in range(5):
    if i == 0 or i == 4:
        new_str = ''
        for char in str_lis[i]:
            if char.lower() not in 'aeiou':
                new_str += char
        new_lis.append(new_str)
    else:
        new_lis.append(str_lis[i])

print('List after removing all the vowels from the first and last strings: ', new_lis)

```

</details>

27. Suppose a list contains 20 integers generated randomly. Receive a number from the keyboard and report position of all occurrences of this number in the list.

<details>

<summary>Solution</summary>

```python
import random
num_lis = [random.randint(1, 10) for i in range(10)]
print(f'List : {num_lis}')
num = int(input('Enter the number to search : '))
count = 0
for i in num_lis:
    if i == num:
        count += 1

print(f'The number of occurrences of {num} is {count}')
```

</details>

28. Suppose a list contains positive and negative numbers. Write a program to create two lists - one containing positive numbers and another containing negative numbers.

<details>

<summary>Solution</summary>

```python
# Take a list of integers as input from the user
num_lis = [int(input('Enter the number : ')) for i in range(10)]

# Create two lists - one containing positive numbers and another containing negative numbers
pos_lis = []
neg_lis = []
for num in num_lis:
    if num >= 0:
        pos_lis.append(num)
    else:
        neg_lis.append(num)

# Print the two lists
print('List of positive numbers:', pos_lis)
print('List of negative numbers:', neg_lis)

```

</details>

29. Take a sentence from user and create a list and print the list of first letter of each word in the first list.

<details>

<summary>Solution</summary>

```python
# Take a sentence from the user as input
sentence = input('Enter a sentence(with spaces only) : ')

# Split the sentence into a list of words
word_list = sentence.split()

# Create a list of the first letter of each word in the sentence
first_letter_list = [word[0] for word in word_list]

# Print the list of first letters
print('List of first letters:', first_letter_list)

```

</details>

30. Create a menu driven python program on **Student Management System** using list.\
    **Options to be in your program**\
    **1. Add**\
    **2. View All Students**\
    **3. Search by name**\
    **4. Search by roll number**\
    **5. Update Students Details**\
    **6. Delete Student**\
    **7. Exit**\
    \&#xNAN;_**Program should ask the user to exit.**_

<details>

<summary>Solution</summary>

```python
# initialize empty student list
students = []

# loop to display menu and get user input
while True:
    print("STUDENT MANAGEMENT SYSTEM")
    print("1. Add student")
    print("2. View all students")
    print("3. Search student by name")
    print("4. Search student by roll number")
    print("5. Update student details")
    print("6. Delete student")
    print("7. Exit")

    # get user input for menu choice
    choice = int(input("Enter your choice (1-7): "))

    if choice == 1:
        # add new student details
        name = input("Enter student name: ")
        rollno = input("Enter student roll number: ")
        marks = input("Enter student marks: ")
        students.append([name, rollno, marks])
        print("Student added successfully!")

    elif choice == 2:
        # view all students
        if len(students) == 0:
            print("No students found!")
        else:
            print("List of students:")
            print("Name\t\tRoll No\t\tMarks")
            for student in students:
                print(f'{student[0]}\t\t{student[1]}\t\t{student[2]}')
                print("")

    elif choice == 3:
        # search student by name
        name = input("Enter student name: ")
        found = False
        for student in students:
            if student[0].lower() == name.lower():
                found = True
                print("Name:", student[0])
                print("Roll No:", student[1])
                print("Marks:", student[2])
                print("")
        if not found:
            print("No student found with name", name)

    elif choice == 4:
        # search student by roll number
        rollno = input("Enter student roll number: ")
        found = False
        for student in students:
            if student[1] == rollno:
                found = True
                print("Name:", student[0])
                print("Roll No:", student[1])
                print("Marks:", student[2])
                print("")
        if not found:
            print("No student found with roll number", rollno)

    elif choice == 5:
        # update student details
        rollno = input("Enter student roll number: ")
        found = False
        for student in students:
            if student[1] == rollno:
                found = True
                print("1. Update name")
                print("2. Update roll number")
                print("3. Update marks")
                subchoice = int(input("Enter your choice (1-3): "))
                if subchoice == 1:
                    name = input("Enter new name: ")
                    student[0] = name
                elif subchoice == 2:
                    rollno = input("Enter new roll number: ")
                    student[1] = rollno
                elif subchoice == 3:
                    marks = input("Enter new marks: ")
                    student[2] = marks
                else:
                    print("Invalid choice!")
        if not found:
            print("No student found with roll number", rollno)

    elif choice == 6:
        # delete student
        rollno = input("Enter student roll number: ")
        found = False
        for student in students:
            if student[1] == rollno:
                found = True
                students.remove(student)
                print("Student deleted successfully!")
        if not found:
            print("No student found with roll number",rollno)
    elif choice == 7:
        # exit program
        print("Thank you for using the Student Management System!")
        break

    else:
        # invalid choice
        print("Invalid choice!")


```

</details>
