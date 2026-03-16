# Loop Assignments

1. **Try to write your name 10 times with the help of a while loop.**

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

```python
name = input('Enter Your Name : ')
i = 1
while(i <= 10):
    print(name)
    i += 1
```

</details>

2. **Design a loop that prints the name of the user 5 times and also the count.**

<details>

<summary>Solution</summary>

```python
i=1
name=input('Enter your name:')
while i<=5:
     print(f'{i}. {name}')
     i=i+1
```

</details>

3. Design a loop that takes 5 values from a user.

<details>

<summary>Solution</summary>

```py
i=1
while i<=5:
    num=int(input('Enter a number:'))
    i=i+1
```

</details>

4\. **Print a simple multiplication table of the number given by user input.**

{% tabs %}
{% tab title="Example" %}
```python
Enter the number: 10
10
20
30
40
50
60
70
80
90
100
```
{% endtab %}
{% endtabs %}

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

<mark style="color:green;">**`num = int(input('Enter the number : '))`**</mark>

<mark style="color:green;">**`i = 1`**</mark>

<mark style="color:green;">**`while(i<=10):`**</mark>

<mark style="color:green;">**`print(num * i)`**</mark>

<mark style="color:green;">**`i = i + 1`**</mark>

</details>

5. **Create a loop that takes 5 values from a user and checks whether each number is even or odd.**

<details>

<summary>Solution</summary>

```py
i=1
while i<=5:
    num=int(input('Enter a number:'))
    if num%2==0:
        print(f'{num} is even')
    else:
        print(f'{num} is odd')
    i=i+1
```

</details>

6. write a program that takes 5 numbers from a user and gives the sum of all the numbers.

<details>

<summary>Solution</summary>

```py
i=1
sum=0
while i<=5:
    num=int(input('Enter a number:')
    sum=sum+num
    i=i+1
print(sum)
```

</details>

7. **Calculate the percentage of a student who has given exams of 5 subjects.**

<details>

<summary>Solution</summary>

```py
i=1
total=0
while i<=5:
    mark=int(input(f'enter marks of subject {i}:'))
    total= total +mark
    i=i+1
print(f'Total Marks:{total}')
per= total*100 / 500
print(f'Percentage:{per}')
```

</details>

8. **Take 10 values from user and find out the sum and multiplication and average of the numbers.**

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

```py
i = 1
s = 0
p = 1
while(i<=10):
    num = int(input('Enter the number : '))
    s = s + num
    p = p * num
    i = i + 1
print(f'Sum is : {s}')
print(f'Product is : {p}')
print(f'Average is {s/(i-1)}')
```

</details>

9. **Do you know Factorial ? It is the product of an integer and all the integers below it; e.g. factorial four (&#x20;**_**4!**_**&#x20;) is equal to 24(4\*3\*2\*1) or factorial of 5 (5!) is equal to 120 (5\*4\*3\*2\*1). Take a number from user and calculate factorial of a number.**

{% tabs %}
{% tab title="Example" %}
**`Enter the number : 6`**

**`Factorial : 120`**
{% endtab %}
{% endtabs %}

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

<pre class="language-py"><code class="lang-py">num = int(input('Enter the number : '))
i = 1
f = 1
while(i&#x3C;=num):
    f = f * i
<strong>    i =i + 1
</strong>print(f)
</code></pre>

</details>

10. **Find all even numbers between 1 to 2000.**

<details>

<summary>Solution</summary>

```python
i=1
while i<=2000:
    if i%2==0:
        print(f'{i} is even')
    i=i+1
```

</details>

11. Write a program to print the even and odd numbers in the range from 1 to n where n is given by the user and also print the sum of all even numbers and odd numbers separately.(use while loop)

<details>

<summary>Solution</summary>

```python
# Ask user to input a number
n = int(input("Enter a number: "))

# Initialize variables
even_sum = 0
odd_sum = 0
i = 1

# Print the even and odd numbers in the range from 1 to n
while i <= n:
    if i % 2 == 0:
        print(i, "is even")
        even_sum += i
    else:
        print(i, "is odd")
        odd_sum += i
    i += 1

# Print the sum of all even and odd numbers separately
print("The sum of all even numbers is", even_sum)
print("The sum of all odd numbers is", odd_sum)

```

</details>

12. **Write a program to check whether a number given by user is prime or not?**\
    **prime number: any number that can be divisible by 1 or self is called prime number. Ex: 2,3,5,7,11,13,17,19 etc**

<details>

<summary>Solution</summary>

<pre class="language-py"><code class="lang-py">num=int(input('Enter a number:')
<strong>divisibility_count=0
</strong>i=1
while i&#x3C;=num:
    if num%i==0:
        divisibility_count+=1
    i=i+1

if divisibility_count==2:
    print(f'{num} is prime')
else:
    print(f'{num} is not prime')
</code></pre>

</details>

13. **Find all prime numbers between 1 to 2000 and their count also.**

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

```python
num=1
prime_num_count=0
while num<=2000:
    divisibility_count=0
    i=1
    while i<=num:
        if num%i==0:
            divisibility_count+=1
        i=i+1

    if divisibility_count==2:
        print(f'{num} is prime')
        prime_num_count+=1
    num=num+1
print(f'Total number of prime numbers:{prime_num_count}')
```

</details>

14. Take a number from user and return the digits of the number.

{% tabs %}
{% tab title="Example" %}
**`Enter The Number : 123`**

**`Digit: 3`**\
**`Digit: 2`**\
**`Digit: 1`**
{% endtab %}
{% endtabs %}

<details>

<summary>Solution</summary>

```py
number = int(input('Enter the number : '))
while(number>0):
    digit = number%10
    print(f'Digit:{digit}')
    number = number // 10
```

</details>

15. Take a number from user and return sum of all digits of the number. Ex: 484= 4+8+4= 16

{% tabs %}
{% tab title="Example" %}
**`Enter The Number : 484`**

**`Sum of the digits : 16`**
{% endtab %}
{% endtabs %}

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

```python
number = int(input('Enter the number : '))
s = 0
while(number>0):
    digit = number%10
    s = s + digit
    number = number // 10
print('Sum of Digits :', s)
```

</details>

16. Take integer inputs from user until he/she presses q ( Ask to press q to quit after every integer input ). Print average and product of all numbers.

{% tabs %}
{% tab title="Example" %}
**`Enter the number : 5`**

**`do you want to quit ? no`**

**`Enter the number : 10`**

**`do you want to quit ? no`**

**`Enter the number : 25`**

**`do you want to quit ? yes`**

**`Sum is 40`**

**`Product is 1250`**
{% endtab %}
{% endtabs %}

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

<mark style="color:green;">**`s = 0`**</mark>

<mark style="color:green;">**`p = 1`**</mark>

<mark style="color:green;">**`while(True):`**</mark>

<mark style="color:green;">**`number = int(input('Enter the number : '))`**</mark>

<mark style="color:green;">**`s = s + number`**</mark>

<mark style="color:green;">**`p = p * number`**</mark>

<mark style="color:green;">**`q = input('do you want to quit ? ').lower()`**</mark>

<mark style="color:green;">**`if(q=='yes'):`**</mark>

<mark style="color:green;">**`break`**</mark>

<mark style="color:green;">**`print(f'Sum is {s}')`**</mark>

<mark style="color:green;">**`print(f'Product is {p}')`**</mark>

</details>

17. A simple iteration through a string to access all elements of it.

<details>

<summary>Solution</summary>

```python
st = input('Enter String : ')
for i in st:
    print(i)
```

</details>

18. Write a Python program that asks the user to enter a sentence and then prints the number of vowels in the sentence.

<details>

<summary>Solution</summary>

```python
sentence = input("Enter a sentence: ")
vowels = "aeiouAEIOU"
count = 0
for char in sentence:
	    if char in vowels:
	        count += 1
print("Number of vowels:", count)

```

</details>

19. Take a string input from user and count the number of vowels and consonants using while loop and for loop both.

<details>

<summary>Solution</summary>

```python
#Using While Loop
st = input('Enter the string : ')
st1 = st.replace(' ', '')
i = 0
vowel_count = 0
cons_count = 0
while(i < len(st1)):
    if st1[i].lower() in 'aeiou':
        vowel_count += 1
    else:
        cons_count += 1
    i += 1
print()
print(f'Original String : {st}')
print(f'Length of string : {len(st)}')
print(f"Vowel's count : {vowel_count}")
print(f"Consonant's count : {cons_count}")

#----------------------------------------------------
#Using for loop
st = input('Enter the string : ')

#Since using for loop we are iterating over string
st1 = st.replace(' ', '')

vowel_count = 0
cons_count = 0

for i in st1:
    if i.lower() in 'aeiou':
        vowel_count += 1
    else:
        cons_count += 1

print()
print(f'Original String : {st}')
print(f'Length of string : {len(st)}')
print(f"Vowel's count : {vowel_count}")
print(f"Consonant's count : {cons_count}")
```

</details>

20. Write a program to count the number of alphabets and no of digits in a string using loops.

<details>

<summary>Solution</summary>

<pre class="language-python"><code class="lang-python">
string = input('Enter any String : ')

alpha_count = 0
digit_count = 0
#Using for loop
for i in string:
    if i.isalpha():
        alpha_count += 1
    elif i.isdigit():
        digit_count += 1
#Using while Loop        
<strong>#i = 0
</strong>#while(i &#x3C; len(string)):
#    if string[i].isalpha():
#        alpha_count += 1
#    elif string[i].isdigit():
#        digit_count += 1 
#    i += 1              
                                
print(f'String : {string} and length : {len(string)}')
print(f'Alphabets count : {alpha_count}')
print(f'Digits Count : {digit_count}')
</code></pre>

</details>

21. Write a program that prints the Fibonacci sequence up to a given number using a while loop.\
    **Example :**\
    **Enter a number : 5**\
    **0 1 1 2 3 5**\
    **Enter a number : 10**\
    0 1 1 2 3 5 8

<details>

<summary>Solution</summary>

```python
# Ask user to input a number
num = int(input("Enter a number: "))

# Initialize variables to store the first two numbers in the sequence
n1, n2 = 0, 1

# Print the Fibonacci sequence up to the given number
while n1 <= num:
    print(n1, end=' ')
    n3 = n1 + n2
    n1 = n2
    n2 = n3

```

</details>

22. Write a python program to check whether a number given by user is a special number or not. _A special number is the number if the sum of the factorial of its digit is same as the original number_. Example : 145 -> factorial of 1 (1) + factorial of 4 (24) + factorial of 5 (120) = 145

<details>

<summary>Solution</summary>

```python
# Ask user to input a number
num = int(input("Enter a number: "))

# Initialize variables
sum = 0
temp = num

# Calculate the sum of factorials of digits
while temp > 0:
    digit = temp % 10
    factorial = 1
    for i in range(1, digit + 1):
        factorial *= i
    sum += factorial
    temp //= 10

# Check if the number is a special number
if num == sum:
    print(num, "is a special number")
else:
    print(num, "is not a special number")

#The Program uses a concept of nested loops.
```

</details>

23. Create a **simple calculator** using **loops** (The program should be menu driven which runs till user exits itself. Means the program must ask the user every time to whether he want to continue or exit). Print Appropriate Message for this.(_**use while() loop**_)

<details>

<summary>Solution</summary>

```python
while True:
    # Display menu options
    print("Calculator Menu:")
    print("1. Addition")
    print("2. Subtraction")
    print("3. Multiplication")
    print("4. Division")
    print("5. Exit")
    
    # Get user choice
    choice = int(input("Enter your choice (1-5): "))
    
    # Perform operation based on user choice
    if choice == 1:
        num1 = int(input("Enter first number: "))
        num2 = int(input("Enter second number: "))
        result = num1 + num2
        print("Result: ", result)
    elif choice == 2:
        num1 = int(input("Enter first number: "))
        num2 = int(input("Enter second number: "))
        result = num1 - num2
        print("Result: ", result)
    elif choice == 3:
        num1 = int(input("Enter first number: "))
        num2 = int(input("Enter second number: "))
        result = num1 * num2
        print("Result: ", result)
    elif choice == 4:
        num1 = int(input("Enter first number: "))
        num2 = int(input("Enter second number: "))
        if num2 == 0:
            print('You Have provided num2 as 0 Division cant perform')
        else:
            result = num1 / num2
            print("Result: ", result)
    elif choice == 5:
        print("Exiting calculator...")
        break
    else:
        print("Invalid choice. Please enter a number between 1 and 5.")
    
    #Program asks to user for exit at option 5

```

</details>

24. Write a program to check whether the number is **`automorphic number`** or not.(_**A number is said to be automorphic number if the original number is present on the right of the square of that number**_.)

**`For example :`**

1\. 5 is an automorphic number as its square is 25 and 5 is at its right side.

2\. Similarly 25 - square 625 and 25 is at its right side.

<details>

<summary>Solution</summary>

```python
# Ask user to input a number
num = int(input("Enter a number: "))

# Calculate the square of the number
square = num * num

# Initialize variables
temp = num
is_automorphic = True
count = 0
#Getting the count of digits of number
while(temp > 0):
    count += 1
    temp //= 10

# Check if the number is an automorphic number

if square%(10 ** (count)) == num:
    print(num, "is an automorphic number")
else:
    print(num, "is not an automorphic number")

```

</details>

25. Write a program to reverse a number taken by the user.

<details>

<summary>Solution</summary>

```python
num = int(input('Enter Number : '))

rev = 0
temp = num

while(temp > 0):
    rev = rev*10 + temp%10
    temp //= 10

print('Original Number :', num)
print('Reversed Number :', rev)

```

</details>

26. Write a program to check whether the number given by the user is an Armstrong number or not.(An Armstrong number is the number whose digits cubes sum is equal to the original number. Such as 153 as 1^3 + 5^3+3^3 = 1 + 125 + 27 = 153)

<details>

<summary>Solution</summary>

```python
# Ask user to input a number
num = int(input("Enter a number: "))

# Initialize variables
temp = num
sum = 0

# Calculate the sum of the cubes of the digits
while temp > 0:
    digit = temp % 10
    sum += digit ** 3
    temp //= 10

# Check if the number is an Armstrong number
if num == sum:
    print(num, "is an Armstrong number")
else:
    print(num, "is not an Armstrong number")

```

</details>

27. Write a program to check whether the given string is palindrome or not.\
    Example : MADAM, MOM

<details>

<summary>Solution</summary>

```python
st = input('Enter the string : ')
revst = ''

i = 0
while(i < len(st)):
    revst += st[len(st)- i - 1]
    i += 1

if revst == st:
    print(st, 'is palindrome')
else:
    print(st, 'is not palindrome')

```

</details>

28. Write a program to check whether the given number is palindrome or not.\
    Example : 343, 121, 111, etc.

<details>

<summary>Solution</summary>

```python
num = int(input('Enter Number : '))

rev = 0
temp = num

while(temp > 0):
    rev = rev*10 + temp%10
    temp //= 10 #Floor Division because division
                #gives float value which will result to inf

if rev == num:
    print(num, 'is palindrome')
else:
    print(num, 'is not palindrome')

```

</details>

29. Create Rock, Paper, Scissor game using while loop\
    (Hint- use random module and random.choice(\['rock', 'paper', 'scissor']) function to get random value selected by computer)\
    Your Program will contain one you and second the computer who will be generating the values from its side using random module.\
    \
    User will provide the choice of Rock, paper or scissor.\
    Print Appropriate Messages and final score of both the computer and user.

<details>

<summary>Solution</summary>

```python
import random as rd
print('Game Instructions'.center(30, '-'))
print('You will get 5 Chance and your score and computer score will be\
      recorded')

comp_score = 0
user_score = 0
chance =  1
while chance <= 5:
    print('Options'.center(10, '-'))
    print('1. Rock'.ljust(5))
    print('2. Paper'.ljust(5))
    print('3. Scissor'.ljust(5))
    ch = int(input('Enter your choice : '))
    comp_ch = rd.choice(['rock', 'paper', 'scissor'])
    if ch == 1:
        print(f'You Selected : rock\nComputer Selected : {comp_ch}')
        if comp_ch == 'rock':
            user_score += 1
            comp_score += 1
            print(f'Tie Your Score : {user_score} and Computer Score : {comp_score}')
        elif comp_ch == 'paper':
            comp_score += 1
            print(f'You Lose Your Score : {user_score} and Computer Score : {comp_score}')
        else:
            user_score += 1
            print(f'Computer Lose Your Score : {user_score} and Computer Score : {comp_score}')
    elif ch == 2:
        print(f'You Selected : paper\nComputer Selected : {comp_ch}')
        if comp_ch == 'paper':
            user_score += 1
            comp_score += 1
            print(f'Tie Your Score : {user_score} and Computer Score : {comp_score}')
        elif comp_ch == 'scissor':
           comp_score += 1
           print(f'You Lose Your Score : {user_score} and Computer Score : {comp_score}')
        else:
           user_score += 1
           print(f'Computer Lose Your Score : {user_score} and Computer Score : {comp_score}')
    elif ch == 3:
         print(f'You Selected : scissor\nComputer Selected : {comp_ch}')
         if comp_ch == 'scissor':
            user_score += 1
            comp_score += 1
            print(f'Tie Your Score : {user_score} and Computer Score : {comp_score}')
         elif comp_ch == 'rock':
           comp_score += 1
           print(f'You Lose Your Score : {user_score} and Computer Score : {comp_score}')
         else:
           user_score += 1
           print(f'Computer Lose Your Score : {user_score} and Computer Score : {comp_score}')
    else:
        print('Wrong Choice Given !!')

    chance += 1
print('Final Score')
print(f'Computer Score : {comp_score}')
print(f'User Score : {user_score}')
if comp_score > user_score:
    print('Computer Won')
elif comp_score < user_score:
    print('You Won')
else:
    print('Match Tie')
print('Thankyou For Playing')

```

</details>

30. Write a Python program that iterates the integers from 1 to 50. For multiples of three print "Fizz" instead of the number and for multiples of five print "Buzz". For numbers that are multiples of three and five, print "FizzBuzz".\
    &#x20;_**Output:**_\
    1\
    2\
    fizz\
    4\
    buzz

<details>

<summary>Solution</summary>

```python
i = 1
while(i <= 50):
    if i %3 == 0 and i % 5 == 0:
        print('FizzBuzz')
    elif i % 5 == 0:
        print('Buzz')
    elif i % 3 ==0:
        print('Fizz')
    else:
        print(i)
    i += 1

```

</details>

31. Write a program to reverse the String using while loop.

<details>

<summary>Solution</summary>

```python
st = input('Enter string : ')
i = 0
revst = ''
while(i < len(st)):
    revst += st[len(st) - i -1]
    i += 1
print(f'Original string : {st}')
print(f'Reversed string : {revst}')

```

</details>

32. Write a Python program to check the validity of passwords input by users.\
    Validation :

* At least 1 letter between \[a-z] and 1 letter between \[A-Z].
* At least 1 number between \[0-9].
* At least 1 character from \[$#@].
* Minimum length 6 characters.
* Maximum length 16 characters.

<details>

<summary>Solution</summary>

```python
# Ask user to input a password
password = input("Enter a password: ")

# Initialize variables to keep track of the password's validity
has_lower = False
has_upper = False
has_digit = False
has_symbol = False
valid_length = False

# Check the password's length
if len(password) >= 6 and len(password) <= 16:
    valid_length = True

# Check if the password contains at least 1 lowercase letter, 1 uppercase letter, 1 digit, and 1 symbol
for char in password:
    if char.islower():
        has_lower = True
    elif char.isupper():
        has_upper = True
    elif char.isdigit():
        has_digit = True
    elif char in "$#@":
        has_symbol = True

# Print the result based on the password's validity
if valid_length and has_lower and has_upper and has_digit and has_symbol:
    print("Password is valid")
else:
    print("Password is not valid")

```

</details>
