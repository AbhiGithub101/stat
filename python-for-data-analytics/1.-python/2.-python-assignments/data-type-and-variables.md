# Data Type & Variables

1. Give a command that displays your introduction in 3 lines.

<details>

<summary>Solution</summary>

```python
print('Hello, i am Dave')
print('I am learning Data Science from Console flare')
print('This is my first assignment')
```

</details>

2. Write a program and create a variable, store an integer value in it, and print the value.
3. Write a program and create three variables called name, age, and company then store your name, your age, and your company's name in it, and

* Print your name, age, and company.
* Now display the message "After 5 Years".
* Now you have switched to another company. Update the company variable and display your new company.

4. Declare a variable and store the value of pi in it. Display the value and check the type of it.

<details>

<summary>Solution</summary>

```python
x=3.14159265
print(x,type(x))
```

</details>

5. Write a program to create two variables a and b which have 2 and 3 as data stored in them. Now create a program that swaps the data which means the data stored in a is 3 and data stored in b is 2.\
   (WITH THE HELP OF A THIRD VARIABLE).

<details>

<summary>Solution</summary>

```python
a=2 
b=3
c=a    # Take a third variable that holds the value of a. c=2
a=b    # a=3
b=c    # b=2
print(a,b)
```

</details>

6. Write a program to create two variables a and b which have 5 and 10 as data stored in them. Now create a program that swaps the data which means the data stored in a is 10 and data stored in b is 5.\
   (WITHOUT USING A THIRD VARIABLE).

<details>

<summary>Solution</summary>

```python
a=5
b=10
a=a+b  # now a is 15      
b=a-b  # now b is 5
a=a-b  # now a is 10
print(a,b)
```

</details>

7. What is wrong in this code snippet?\
   a,b,c=1,2

* Nothing is wrong
* The value of c is missing
* Wrong syntax
* None of the above

<details>

<summary>Solution</summary>

Value of c is missing.

</details>

8. a,b,c=22,33,78\
   print(a,c)\
   What will be the output of this code?

* 22,78
* 22,33,78
* 33,78
* 22,33

<details>

<summary>Solution</summary>

22,78

</details>

9. You have to create three variables A, B, and C. Store 2000 in all of them. This task can be done by two methods:\
   \
   a. A=B=C=2000\
   b. A, B, C=2000,2000,2000\
   c. a and b both\
   d. None of the above\
   e. A, B, C=2000

<details>

<summary>Solution</summary>

c

</details>

10. What will be the output of the following code?\
    x = 10\
    y = 5.5\
    z = "10"\
    print(type(x), type(y), type(z))

<details>

<summary>Solution</summary>

```python
<class 'int'> <class 'float'> <class 'str'>
```

</details>

11. Check the data type of the following:\
    a. 2+3\
    b. '56+78'\
    c. 'True + False \* 0'\
    d. 32+0.0\
    e. 7834+57.23

<details>

<summary>Solution</summary>

```python
print(type(2+3))
print(type('56+78'))
print(type( 'True + False * 0'))
print(type(32+0.0))
print(type(7834+57.23))
```

</details>
