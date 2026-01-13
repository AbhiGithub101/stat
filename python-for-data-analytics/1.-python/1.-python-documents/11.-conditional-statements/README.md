# 11. Conditional Statements

**What are Conditional Statements?**

We have often used conditional statements in our daily life, such as :

**if** _it rains_ ,i will go to office.

**Syntax:**

In \[ ]:

```
if expression:  
    statement  
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2Fk7vQ1SkZnfI3Ae0GP4uZ%2Fimage.png?alt=media&#x26;token=4684f90c-475c-4e65-a38f-64b728e987b7" alt=""><figcaption></figcaption></figure>

Above Figure Shows , Actions or decisions based on the Condition. If the condition is True, i will not go to office. Here are some Examples for if statement:

**How to Find if a number is even?**

In \[2]:

```
number = int(input("Enter the number:"))

if(number%2==0):
    print(f'{number} is an even number')
    print(f'{number} is not an odd number')

print("Program ended")
```

```
Enter the number:10
10 is an even number
10 is not an odd number
Program ended
```

### Indentation:

Python indentation is a way of telling python intrepreter that the group of statements/code/instrtuctions belong to a particular block.

In more simpler terms , indentation is nothing but a bunch of spaces or tabs signifying a particular line of code belongs to a same group.

Now You saw what will happen if the condition is true in above case. All the code with same indentation will run. But what will happen if the condition is False?

In \[3]:

```
number = int(input("Enter the number:"))

if(number%2==0):
    print(f'{number} is an even number')
    print(f'{number} is not an odd number')

print("Program ended")
```

```
Enter the number:15
Program ended
```

So, Here the codes with same indentation did not run, it shows that if condition is True, Body of if will run. Body of if (Codes written under if statement by using indentation.), if Condition is False, Body of if will not run.

**Note:**&#x57;e generally use Tab to define indentations. One Tab means 4 spaces.

### if-else statement:

The if-else statement is similar to if statement except the fact that, it also provides the block of the code for the false case of the condition to be checked.

If the condition provided in the if statement is false, then the else statement will be executed.

For Example : . **if** coffee house is open i'll go there **else** i will be at home.

In \[ ]:

```
if condition:  
    #block of statements   
else:   
    #another block of statements (else-block)  
```

**To find if a number is even or odd:**

In \[2]:

```
number = int(input("Enter the number:"))

if(number%2==0):
    print(f'{number} is an even number')
else:
    print(f'{number} is an odd number')
```

```
Enter the number:10
10 is an even number
```

In \[3]:

```
number = int(input("Enter the number:"))

if(number%2==0):
    print(f'{number} is an even number')
else:
    print(f'{number} is an odd number')
```

```
Enter the number:15
15 is an odd number
```

### if-elif statement:

The elif statement enables us to check multiple conditions and execute the specific block of statements depending upon what condition is True.

**Syntax:**

In \[ ]:

```
if expression 1:   
    # block of statements   
  
elif expression 2:   
    # block of statements   
  
elif expression 3:   
    # block of statements   
  
else:   
    # block of statements 
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FHf6HCbSuI96TK1hO2IxP%2Fimage.png?alt=media&#x26;token=b5a4baa1-dbb0-4de9-9c4a-677e9a605b57" alt=""><figcaption></figcaption></figure>

So , elif - statement , in more simpler terms runs body of first if or elif statement with true condition and if any of the condition is not true , body of else executes.

For Example:

**Program to find grade of a student based on marks:**

In \[1]:

```
marks = int(input("Please enter the marks:")) 

if(marks>90):
    grade = "A"
elif(marks>70):
    grade="B"
elif(marks>50):
    grade = "C"
elif(marks>30):
    grade = "D"
else:
    grade = "F"

print(f"your grade : {grade}")
```

```
Please enter the marks:40
your grade : D
```

### Nested if:

There may be a situation when you want to check for another condition after a condition resolves to true. In such a situation, you can use the nested if construct.

In more simpler terms, Nested if is actually if statement under an if statement.

**Syntax:**

In \[ ]:

```
if expression 1:   
    # block of statements   
  
    if expression 2:   
        # block of statements   
  
        if expression 3:   
            # block of statements   
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FN4yLwsvuhbLjcEEB5A5N%2Fimage.png?alt=media&#x26;token=76d5018f-10d6-45df-a4fc-ea2a640b6ae3" alt=""><figcaption></figcaption></figure>

**Program to find Largest Number among three numbers:**

In \[1]:

```
a = int(input("enter the number:"))
b = int(input("enter the number:"))
c = int(input("enter the number:"))

if(a>b):
    if(a>c):
        large = a
    else:
        large = c
else:
    if(b>c):
        large = b
    else:
        large = c

print("Largest Number is: ", c)
```

```
enter the number:5
enter the number:10
enter the number:15
Largest Number is:  15
```

**Note:** Run above code in your editor and change values to see , how this code is working.

## Branching using Conditional Statements in Python

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FEVHDoY6GNcLJXc9qC6Sp%2Fimage.png?alt=media&#x26;token=1108c8bc-3862-4966-ae30-c9ff7b61051d" alt=""><figcaption></figcaption></figure>

This tutorial covers the following topics:

* Branching with `if`, `else` and `elif`
* Nested conditions and `if` expressions
* Iteration with `while` loops
* Iterating over containers with `for` loops
* Nested loops, `break` and `continue` statements

#### Branching with `if`, `else` and `elif`

One of the most powerful features of programming languages is _branching_: the ability to make decisions and execute a different set of statements based on whether one or more conditions are true.

**The `if` statement**

In Python, branching is implemented using the `if` statement, which is written as follows:

```
if condition:
    statement1
    statement2
```

The `condition` can be a value, variable or expression. If the condition evaluates to `True`, then the statements within the _`if` block_ are executed. Notice the four spaces before `statement1`, `statement2`, etc. The spaces inform Python that these statements are associated with the `if` statement above. This technique of structuring code by adding spaces is called _indentation_.

> **Indentation**: Python relies heavily on _indentation_ (white space before a statement) to define code structure. This makes Python code easy to read and understand. You can run into problems if you don't use indentation properly. Indent your code by placing the cursor at the start of the line and pressing the `Tab` key once to add 4 spaces. Pressing `Tab` again will indent the code further by 4 more spaces, and press `Shift+Tab` will reduce the indentation by 4 spaces.

For example, let's write some code to check and print a message if a given number is even.

```
a_number = 34
```

```
if a_number % 2 == 0:
    print("We're inside an if block")
    print(f'The given number {a_number} is even.')
```

```
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-1-e8e68e9c1a14> in <module>
----> 1 if a_number % 2 == 0:
      2     print("We're inside an if block")
      3     print(f'The given number {a_number} is even.')

NameError: name 'a_number' is not defined
```

We use the modulus operator `%` to calculate the remainder from the division of `a_number` by `2`. Then, we use the comparison operator `==` check if the remainder is `0`, which tells us whether the number is even, i.e., divisible by 2.

Since `34` is divisible by `2`, the expression `a_number % 2 == 0` evaluates to `True`, so the `print` statement under the `if` statement is executed. Also, note that we are using the string `format` method to include the number within the message.

Let's try the above again with an odd number.

```
another_number = 33
```

In \[4]:

```
if another_number % 2 == 0:
    print(f'The given number {a_number} is even.')
```

As expected, since the condition `another_number % 2 == 0` evaluates to `False`, no message is printed.

**The `else` statement**

We may want to print a different message if the number is not even in the above example. This can be done by adding the `else` statement. It is written as follows:

```
if condition:
    statement1
    statement2
else:
    statement4
    statement5
```

If `condition` evaluates to `True`, the statements in the `if` block are executed. If it evaluates to `False`, the statements in the `else` block are executed.

In \[5]:

```
a_number = 34
```

In \[6]:

```
if a_number % 2 == 0:
    print(f'The given number {a_number} is even.')
else:
    print(f'The given number {a_number} is odd.')
```

```
The given number 34 is even.
```

In \[7]:

```
another_number = 33
```

In \[8]:

```
if another_number % 2 == 0:
    print(f'The given number {another_number} is even.')
else:
    print(f'The given number {another_number} is odd.')
```

```
The given number 33 is odd.
```

Here's another example, which uses the `in` operator to check membership within a tuple.

In \[9]:

```
the_3_musketeers = ('Athos', 'Porthos', 'Aramis')
```

In \[10]:

```
a_candidate = "D'Artagnan"
```

In \[11]:

```
if a_candidate in the_3_musketeers:
    print(f"{a_candidate} is a musketeer")
else:
    print(f"{a_candidate} is not a musketeer")
```

```
D'Artagnan is not a musketeer
```

**The `elif` statement**

Python also provides an `elif` statement (short for "else if") to chain a series of conditional blocks. The conditions are evaluated one by one. For the first condition that evaluates to `True`, the block of statements below it is executed. The remaining conditions and statements are not evaluated. So, in an `if`, `elif`, `elif`... chain, at most one block of statements is executed, the one corresponding to the first condition that evaluates to `True`.

In \[12]:

```
today = 'Wednesday'
```

In \[13]:

```
if today == 'Sunday':
    print("Today is the day of the sun.")
elif today == 'Monday':
    print("Today is the day of the moon.")
elif today == 'Tuesday':
    print("Today is the day of Tyr, the god of war.")
elif today == 'Wednesday':
    print("Today is the day of Odin, the supreme diety.")
elif today == 'Thursday':
    print("Today is the day of Thor, the god of thunder.")
elif today == 'Friday':
    print("Today is the day of Frigga, the goddess of beauty.")
elif today == 'Saturday':
    print("Today is the day of Saturn, the god of fun and feasting.")
```

```
Today is the day of Odin, the supreme diety.
```

In the above example, the first 3 conditions evaluate to `False`, so none of the first 3 messages are printed. The fourth condition evaluates to `True`, so the corresponding message is printed. The remaining conditions are skipped. Try changing the value of `today` above and re-executing the cells to print all the different messages.

To verify that the remaining conditions are skipped, let us try another example.

In \[14]:

```
a_number = 15
```

```
if a_number % 2 == 0:
    print(f'{a_number} is divisible by 2')
elif a_number % 3 == 0:
    print(f'{a_number} is divisible by 3')
elif a_number % 5 == 0:
    print(f'{a_number} is divisible by 5')
elif a_number % 7 == 0:
    print(f'{a_number} is divisible by 7')
```

```
15 is divisible by 3
```

Note that the message `15 is divisible by 5` is not printed because the condition `a_number % 5 == 0` isn't evaluated, since the previous condition `a_number % 3 == 0` evaluates to `True`. This is the key difference between using a chain of `if`, `elif`, `elif`... statements vs. a chain of `if` statements, where each condition is evaluated independently.

In \[16]:

```
if a_number % 2 == 0:
    print(f'{a_number} is divisible by 2')
if a_number % 3 == 0:
    print(f'{a_number} is divisible by 3')
if a_number % 5 == 0:
    print(f'{a_number} is divisible by 5')
if a_number % 7 == 0:
    print(f'{a_number} is divisible by 7')
```

```
15 is divisible by 3
15 is divisible by 5
```

**Using `if`, `elif`, and `else` together**

You can also include an `else` statement at the end of a chain of `if`, `elif`... statements. This code within the `else` block is evaluated when none of the conditions hold true.

In \[17]:

```
a_number = 49
```

```
if a_number % 2 == 0:
    print(f'{a_number} is divisible by 2')
elif a_number % 3 == 0:
    print(f'{a_number} is divisible by 3')
elif a_number % 5 == 0:
    print(f'{a_number} is divisible by 5')
else:
    print('All checks failed!')
    print(f'{a_number} is not divisible by 2, 3 or 5')
```

```
All checks failed!
49 is not divisible by 2, 3 or 5
```

In \[19]:

```
a_number = 12
```

In \[20]:

```
if a_number % 3 == 0 and a_number % 5 == 0:
    print(f"The number {a_number} is divisible by 3 and 5")
elif not a_number % 5 == 0:
    print(f"The number {a_number} is not divisible by 5")
```

```
The number 12 is not divisible by 5
```

**Non-Boolean Conditions**

Note that conditions do not necessarily have to be booleans. In fact, a condition can be any value. The value is converted into a boolean automatically using the `bool` operator. This means that falsy values like `0`, `''`, `{}`, `[]`, etc. evaluate to `False` and all other values evaluate to `True`.

In \[21]:

```
if '':
    print('The condition evaluted to True')
else:
    print('The condition evaluted to False')
```

```
The condition evaluted to False
```

In \[22]:

```
if 'Hello':
    print('The condition evaluted to True')
else:
    print('The condition evaluted to False')
```

```
The condition evaluted to True
```

In \[23]:

```
if { 'a': 34 }:
    print('The condition evaluted to True')
else:
    print('The condition evaluted to False')
```

```
The condition evaluted to True
```

In \[24]:

```
if None:
    print('The condition evaluted to True')
else:
    print('The condition evaluted to False')
```

```
The condition evaluted to False
```

**Nested conditional statements**

The code inside an `if` block can also include an `if` statement inside it. This pattern is called `nesting` and is used to check for another condition after a particular condition holds true.

In \[25]:

```
a_number = 15
```

In \[26]:

```
if a_number % 2 == 0:
    print(f"{a_number} is even")
    if a_number % 3 == 0:
        print(f"{a_number} is also divisible by 3")
    else:
        print(f"{a_number} is not divisibule by 3")
else:
    print(f"{a_number} is odd".format(a_number))
    if a_number % 5 == 0:
        print(f"{a_number} is also divisible by 5")
    else:
        print(f"{a_number} is not divisibule by 5")
```

```
15 is odd
15 is also divisible by 5
```

Notice how the `print` statements are indented by 8 spaces to indicate that they are part of the inner `if`/`else` blocks.

> Nested `if`, `else` statements are often confusing to read and prone to human error. It's good to avoid nesting whenever possible, or limit the nesting to 1 or 2 levels.

**Shorthand `if` conditional expression**

A frequent use case of the `if` statement involves testing a condition and setting a variable's value based on the condition.

```
a_number = 13

if a_number % 2 == 0:
    parity = 'even'
else:
    parity = 'odd'

print(f'The number {a_number} is {parit}.')
```

```
The number 13 is odd.
```

Python provides a shorter syntax, which allows writing such conditions in a single line of code. It is known as a _conditional expression_, sometimes also referred to as a _ternary operator_. It has the following syntax:

```
x = true_value if condition else false_value
```

It has the same behavior as the following `if`-`else` block:

```
if condition:
    x = true_value
else:
    x = false_value
```

Let's try it out for the example above.

In \[28]:

```
parity = 'even' if a_number % 2 == 0 else 'odd'
```

In \[29]:

```
print('The number {a_number} is {parity}.')
```

```
The number 13 is odd.
```

**Statements and Expressions**

The conditional expression highlights an essential distinction between _statements_ and _expressions_ in Python.

> **Statements**: A statement is an instruction that can be executed. Every line of code we have written so far is a statement e.g. assigning a variable, calling a function, conditional statements using `if`, `else`, and `elif`, loops using `for` and `while` etc.
>
> **Expressions**: An expression is some code that evaluates to a value. Examples include values of different data types, arithmetic expressions, conditions, variables, function calls, conditional expressions, etc.

Most expressions can be executed as statements, but not all statements are expressions. For example, the regular `if` statement is not an expression since it does not evaluate to a value. It merely performs some branching in the code. Similarly, loops and function definitions are not expressions (we'll learn more about these in later sections).

As a rule of thumb, an expression is anything that can appear on the right side of the assignment operator `=`. You can use this as a test for checking whether something is an expression or not. You'll get a syntax error if you try to assign something that is not an expression.

In \[30]:

```
# if statement
result = if a_number % 2 == 0: 
    'even'
else:
    'odd'
```

```
 File "<ipython-input-30-f24978c5423e>", line 2
    result = if a_number % 2 == 0:
             ^
SyntaxError: invalid syntax
```

In \[31]:

```
# if expression
result = 'even' if a_number % 2 == 0 else 'odd'
```

**The `pass` statement**

`if` statements cannot be empty, there must be at least one statement in every `if` and `elif` block. You can use the `pass` statement to do nothing and avoid getting an error.

```
a_number = 9
```

In \[33]:

```
if a_number % 2 == 0:
elif a_number % 3 == 0:
    print(f'{a_number} is divisible by 3 but not divisible by 2')
```

```
  File "<ipython-input-33-77268dd66617>", line 2
    elif a_number % 3 == 0:
    ^
IndentationError: expected an indented block
```

In \[34]:

```
if a_number % 2 == 0:
    pass
elif a_number % 3 == 0:
    print(f'{a_number} is divisible by 3 but not divisible by 2')
```

```
9 is divisible by 3 but not divisible by 2
```

#### Questions for Revision

Try answering the following questions to test your understanding of the topics covered in this notebook:

1. What is branching in programming languages?
2. What is the purpose of the `if` statement in Python?
3. What is the syntax of the `if` statement? Give an example.
4. What is indentation? Why is it used?
5. What is an indented block of statements?
6. How do you perform indentation in Python?
7. What happens if some code is not indented correctly?
8. What happens when the condition within the `if` statement evaluates to `True`? What happens if the condition evaluates for `false`?
9. How do you check if a number is even?
10. What is the purpose of the `else` statement in Python?
11. What is the syntax of the `else` statement? Give an example.
12. Write a program that prints different messages based on whether a number is positive or negative.
13. Can the `else` statement be used without an `if` statement?
14. What is the purpose of the `elif` statement in Python?
15. What is the syntax of the `elif` statement? Give an example.
16. Write a program that prints different messages for different months of the year.
17. Write a program that uses `if`, `elif`, and `else` statements together.
18. Can the `elif` statement be used without an `if` statement?
19. Can the `elif` statement be used without an `else` statement?
20. What is the difference between a chain of `if`, `elif`, `elif`… statements and a chain of `if`, `if`, `if`… statements? Give an example.
21. Can non-boolean conditions be used with `if` statements? Give some examples.
22. What are nested conditional statements? How are they useful?
23. Give an example of nested conditional statements.
24. Why is it advisable to avoid nested conditional statements?
25. What is the shorthand `if` conditional expression?
26. What is the syntax of the shorthand `if` conditional expression? Give an example.
27. What is the difference between the shorthand `if` expression and the regular `if` statement?
28. What is a statement in Python?
29. What is an expression in Python?
30. What is the difference between statements and expressions?
31. Is every statement an expression? Give an example or counterexample.
32. Is every expression a statement? Give an example or counterexample.
