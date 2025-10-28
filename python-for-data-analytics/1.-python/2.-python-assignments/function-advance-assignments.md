# Function - Advance Assignments

1. Write a program to create a function which take your name and greet you.

<details>

<summary>Solution</summary>

```python
def greet(name):
    print('Hello,', name)
your_name = input('Enter your name : ')
greet(your_name)
```

</details>

2. Write a program to take two values and print the sum using function.

<details>

<summary>Solution</summary>

```python
def add(a, b):
    print('Sum  =', (a + b))
    
a = int(input('Enter a : '))
b = int(input('Enter b : '))

add(a, b)
```

</details>

3. Write a Python program to print the multiplication table of a given number(**using functions**).

<details>

<summary>Solution</summary>

```python
def printTable(num):
    for i in range(1, 11):
        print(f'{num} x {i} = {num * i}')

number = int(input('Enter number : '))
printTable(number)
```

</details>

4. Write a python program to create a function **area\_of\_square(side)** and calculate the area of square through taking input from user.

<details>

<summary>Solution</summary>

```python
def area_of_square(side):
    print(f'Area of square of side {side} is {side ** 2}')
    
side = int(input('Enter side : '))
area_of_square(side)
```

</details>

5. Write a program to create a function to calculate the area of rectangle and the function must return the value.

<details>

<summary>Solution</summary>

```python
def area_rect(length, breadth):
    return length * breadth
    
print('Area of Rectangle of length 10 and breadth 20 : ', area_rect(10, 20))
```

</details>

6. Write a program to receive three integers from keyboard and get their sum and product calculated through a user-defined function **cal\_sum\_prod().**

<details>

<summary>Solution</summary>

```python
def cal_sum_prod(x, y, z):
    s = x + y + z
    p = x * y * z
    print(f'Sum of {x}, {y} and {z} is {s}')
    print(f'Sum of {x}, {y} and {z} is {p}')
    
cal_sum_prod(2, 3, 5)
```

</details>

7. Write a python program to find the sum of all the even numbers between the range of `start` and `end` using functions.

<details>

<summary>Solution</summary>

```python
def sum_even_numbers(start, end):
    sum = 0
    for num in range(start, end+1):
        if num % 2 == 0:
            sum += num
    return sum

start = 1
end = 50

print("The sum of even numbers between", start, "and", end, "is", sum_even_numbers(start, end))

```

</details>

8. Write a python program to check if the given number is even or odd using functions.

<details>

<summary>Solution</summary>

```python
#using return type
def check_even_odd(num):
    if num % 2 ==0:
        return True
    else:
        return False
        
print('5 is even :', check_even_odd(5))
#-------------------------------------------
#using without return type
def check_even_odd(num):
    if num % 2 == 0:
        print(num, 'is even')
    else:
        print(num, 'is odd')
check_even_odd(5)
check_even_odd(6)
```

</details>

9. Pangram is a sentence that uses every letter of the alphabet. Write a program that checks whether a given string is pangram or not, through a user-defined function **ispangram()**

<details>

<summary>Solution</summary>

```python
def ispangram(string):
    alphaset = set('abcdefghijklmnopqrstuvwxyz')
    string_set = set(string.replace(' ', '').lower())
    if alphaset.issubset(string_set):
        print('String is Pangram')
    else:
        print('String is not pangram')
        
ispangram('The quick brown fox jumps over the lazy dog')
ispangram('Consoleflare is good place to learn data science')
ispangram('Crazy Fredrick bought many very exquisite opal jewels')
```

</details>

10. Write a python program to get the reverse of the string using functions.

<details>

<summary>Solution</summary>

```python
def reverse_string(string):
    return string[::-1]
print(reverse_string('consoleflare'))
```

</details>

11. Write a python program that accepts a hypen-separated sequence of words as input and calls a function **convert()** which converts it into a hypen-separated sequence _**after sorting them alphabetically.**_ For example, if the input string is\
    \
    \&#xNAN;**'here-come-the-dots-followed-by-dashes'**\
    \&#xNAN;_**then the converted string should be**_\
    **by-come-dashes-dots-followed-here-the**

<details>

<summary>Solution</summary>

```python
def convert(s):
    words = s.split('-')
    words.sort()
    return '-'.join(words)
print(convert('here-come-the-dots-followed-by-dashes'))
```

</details>

12. Write a python function to create and return a list containing tuples of the form (x, x^2, x^3) for all x between 1 and 20(both included).

<details>

<summary>Solution</summary>

```python
def generate_list():
    lst = []
    for i in range(1, 21):
        lst.append((i, i**2, i**3))
    return lst
l = generate_list()
print(l)
```

</details>

13. A palindrome is a word or phrase which reads the same in both directions. Given below are some palindromic strings:\
    **deed**\
    **level**\
    **Malayalam**\
    **Rats live on no evil star**\
    **Murder for a jar of red rum**\\
14. Write a program that defines a function **ispalindrome()** which checks whether a given string is a palindrome or not. Ignore spaces and case mismatch while checking for palindrome.

<details>

<summary>Solution</summary>

```python
def ispalindrome(s):
    st = s.lower().replace(' ', '')
    return st == st[::-1]
print(ispalindrome('deed'))
print(ispalindrome('level'))
print(ispalindrome('Malayalam'))
print(ispalindrome('Rats live on no evil star'))
print(ispalindrome('Murder for a jar of red rum'))
print(ispalindrome('consoleflare'))
```

</details>

15. Write a program that defines a function **convert()** that receives a string containing a sequence of whitespace separated words and returns a string after removing all duplicate words and sorting them alphnumerically.\
    For example if the string passed to **convert()** is\
    s = 'Sakhi was a singer because her mother was a singer, and Sakhi\\'s mother was a singer because her father was a singer'.\
    \
    **then, the output should be :**\
    **Sakhi Sakhi's and because father her mother singer singer, was**

<details>

<summary>Solution</summary>

```python
def convert(s):
    words = s.split()
    return ' '.join(sorted(list(set(words))))
s = input('Enter a string : ')
print(s)
print(convert(s))
```

</details>

16. Write a program that defines a function **count\_alphabets\_digits()** that accepts a string and calculates the number of alphabets and digits in it. It should return these values as a dictionary. Call this function for some sample strings.

<details>

<summary>Solution</summary>

```python
def count_alphabets_digits(s):
    d = {'Digits':0, 'Alphabets':0}
    for ch in s:
        if ch.isalpha():
            d['Alphabets'] += 1
        elif ch.isdigit():
            d['Digits'] += 1
    return d
d = count_alphabets_digits('James Bond 007')
print(d)
d = count_alphabets_digits('Kholi Number 420')
print(d)
```

</details>

17. Write a program that defines a function called **frequency()** which computes the frequency of words present in a string passed to it. The frequencies should be returned in sorted order by words in the string.

<details>

<summary>Solution</summary>

```python
def frequency(s):
    freq = {}
    for word in s.split():
        freq[word] = freq.get(word, 0) + 1
    return freq
s = input('Enter string : ')
d = frequency(s)
words = sorted(d)

for key in words:
    print(f'{key} : {d[key]}')
```

</details>

18. Write a Python program to find the factorial of a number using **functions.**

<details>

<summary>Solution</summary>

```python
def factorial(num):
    fact = 1:
    for i in range(1, num + 1):
        fact = fact * i
        
    print(f'Factorial of {num} is {fact}')
    
factorial(5)
factorial(4)
```

</details>

19. Write a python program to check whether the number is prime or not using functions.

<details>

<summary>Solution</summary>

```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(n/2)+1):
        if n % i == 0:
            return False
    return True

num = int(input("Enter a number: "))
if is_prime(num):
    print(num, "is a prime number")
else:
    print(num, "is not a prime number")
```

</details>

20. Write a Python program to count the number of vowels in a string.

<details>

<summary>Solution</summary>

```python
def count_vowels(s):
    vowels = 'aeiou'
    count = 0
    for char in s:
        if char.lower() in vowels:
            count += 1
    return count

st = input("Enter a string: ")
print("Number of vowels in", st, "is", count_vowels(st))
```

</details>

21. Write a Python function to find the sum of the digits of a given number.

<details>

<summary>Solution</summary>

```python
def sum_of_digits(number):
    """
    This function takes a number as input and returns the sum of its digits.
    """
    sum = 0
    while number > 0:
        digit = number % 10
        sum += digit
        number //= 10
    return sum

number = int(input('Enter Number : '))
print("The sum of digits of", number, "is", sum_of_digits(number))
```

</details>

22. Write a python program to take multiple number of variables but the number of arguments are not fixed they may vary and calculate the sum of those numbers. **It is provided that the values passed must be numbers.**

<details>

<summary>Solution</summary>

```python
def sum_all(*args):
    """
    This function takes any number of arguments and returns their sum.
    """
    sum = 0
    for arg in args:
        sum += arg
    return sum

print(sum_all(1, 2, 3, 4, 5))  # Output: 15
print(sum_all(10, 20, 30))    # Output: 60
print(sum_all(1, 3, 5, 7))    # Output: 16
```

</details>

23. Write a Python program that takes a list of numbers as input and outputs the range of the list (i.e. the difference between the largest and smallest values).

<details>

<summary>Solution</summary>

```python
def find_range(numbers):
    """
    This function takes a list of numbers as input and returns the range of the list.
    """
    min_num = min(numbers)
    max_num = max(numbers)
    return max_num - min_num

numbers = [1, 2, 3, 4, 5]
print(find_range(numbers))  # Output: 4

numbers = [-10, 0, 10, 20, 30]
print(find_range(numbers))  # Output: 40

numbers = [5, 5, 5, 5, 5]
print(find_range(numbers))  # Output: 0
```

</details>

24. Write a Python function that takes a list of numbers as input and returns a new list containing only the even numbers from the input list.

<details>

<summary>Solution</summary>

```python
def even_numbers(numbers):
    """
    This function takes a list of numbers as input and returns a new list containing only the even numbers.
    """
    even_numbers_list = []
    for num in numbers:
        if num % 2 == 0:
            even_numbers_list.append(num)
    return even_numbers_list

numbers = [1, 2, 3, 4, 5, 6]
print(even_numbers(numbers))  # Output: [2, 4, 6]

numbers = [10, 15, 20, 25, 30]
print(even_numbers(numbers))  # Output: [10, 20, 30]

numbers = [7, 13, 17, 21, 25]
print(even_numbers(numbers))  # Output: []
```

</details>

25. Write a Python function that takes a list of strings as input and returns a new list containing only the strings that start with the letter 'A'.

<details>

<summary>Solution</summary>

```python
def filter_strings(strings):
    """
    This function takes a list of strings as input and returns a new list containing only the strings that start with the letter 'A'.
    """
    result = []
    for s in strings:
        if s.startswith('A') or s.startswith('a'):
            result.append(s)
    return result

strings = ['Apple', 'Banana', 'Apricot', 'Cherry', 'avocado']
print(filter_strings(strings))  # Output: ['Apple', 'Apricot', 'avocado']

strings = ['Ant', 'Bat', 'Ape', 'Alligator', 'bee']
print(filter_strings(strings))  # Output: ['Ant', 'Ape', 'Alligator']
```

</details>

26. Write a Python function that takes a list of numbers as input and returns the average of all the numbers in the list.

<details>

<summary>Solution</summary>

```python
def calculate_average(numbers):
    """
    This function takes a list of numbers as input and returns their average.
    """
    if len(numbers) == 0:
        return None
    return sum(numbers) / len(numbers)

numbers = [2, 4, 6, 8, 10]
print(calculate_average(numbers))  # Output: 6.0

numbers = []
print(calculate_average(numbers))  # Output: None

numbers = [3, 5, 7]
print(calculate_average(numbers))  # Output: 5.0
```

</details>
