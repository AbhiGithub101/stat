# Conditional Statements Assignments

### Questions Using If - else block

1. In a classic chase, Tom is running after Jerry as Jerry has eaten Tom's favourite food.

Jerry is running at a speed of $$X$$ metres per second while Tom is chasing him at a speed of $$Y$$ metres per second. Determine whether Tom will be able to catch Jerry.

Note that initially Jerry is not at the same position as Tom.\
\
Take X of Jerry and Y of Tom from the user and make decision and\
print YES if tom can catch and NO if not.\
\
**Sample Input**

```
2 3
4 1
1 1
3 5
```

**Sample Output**

```
YES
NO
NO
YES
```

<details>

<summary>Solution</summary>

```python
x = int(input('Enter Jerry Speed : '))
y = int(input('Enter Tom Speed : '))

if y > x:
    print('YES')
else:
    print('NO')
```

</details>

2. Apple considers any iPhone with a battery health of $$80%$$% or above, to be in _optimal_ condition.

Given that your iPhone has $$X%$$%battery health, find whether it is in _optimal_ condition.

Take Battery Health from User and print YES if in optimal condition and NO if not.\
**Sample Input**&#x20;

```
97
42
80
10
```

**Sample Output**

```
YES
NO
YES
NO
```

<details>

<summary>Solution</summary>

```python
x = int(input('Enter Battery health : '))
if x >= 80:
    print('YES')
else:
    print('NO')
```

</details>

3. While purchasing certain items, a discount of 10 % is offered if the quantity purchased is more than 1000. If quantity and price per item are input through the keyboard, write a program to calculate the total expenses.

<details>

<summary>Solution</summary>

```python
qty = int(input(‘Enter the value of quantity : ’))
price  = int(input(‘Enter the Price : ’))
dis = 0
if qty > 1000:
	dis=  10
else:
	dis = 0

Totexp = qty*price-qty*price*dis/100
print(f‘Total Expense : Rs {Totexp}’)

```

</details>

4. A company decided to give bonus of 5% to employee if his/her year of service is more than 5 years. Ask user for their salary and year of service and print the net bonus amount.

<details>

<summary>Solution</summary>

```python
salary = float(input("Enter salary : "))
yos = int(input("Enter year of service : "))
if yos>5:
  print("Bonus is",(5/100)*salary)
else:
  print("No bonus")

```

</details>

5. A University allows students to sit in the exam despite of insufficient attendance if the student's attendance is short due to some medical cause. Take Input from User whether he had medical cause (Y/N) and print the message _you are allowed_ **if medical cause == Y** otherwise print _you are not allowed._

<details>

<summary>Solution</summary>

```python
medical_cause = input('Input Whether you had any medical cause or not (Y/N)')
if medical_cause == 'Y':
    print('You are allowed')
else:
    print('You are not allowed')
```

</details>

6. Write a program to check whether the last digit of the number is divisible by 3 or not.\
   **Take Number from user and your output must contain the number**.

<details>

<summary>Solution</summary>

```python
number = int(input('Enter Number : '))
if (number%10)%3 == 0:
    print(f'{number} is divisble by 3')
else:
    print(f'{number} is not divisible by 3')
```

</details>

7. Write a program to display ‘Hello’ if the number entered by user is multiple of 5 otherwise prints ‘Bye’.

<details>

<summary>Solution</summary>

```python
num = int(input('Enter the number : '))
if num % 5 == 0:
    print('Hello')
else:
    print('Bye')
```

</details>

8. **Write a program to check whether a person is eligible for voting or not.(voting age >=18)**

<details>

<summary>Solution</summary>

```python
age = int(input('Enter age : '))
if age >= 18:
    print('Eligible')
else:
    print('Not Eligible')
```

</details>

9. **Write a program to check whether a number entered by user is even or odd.**

<details>

<summary>Solution</summary>

```python
num = int(input("Enter the number : "))
if num %2 == 0:
    print(f'{num} is even')
else:
    print(f'{num} is odd')
```

</details>

10. **Write a program to check whether a given character is a vowel or a consonant.**

<details>

<summary>Solution</summary>

```python
char = input("Enter a character: ")
if char in "AEIOUaeiou":
    print(char, "is a vowel")
else:
    print(char, "is a consonant")
```

</details>

11. **Write a program to check whether a given string is a valid email address&#x20;**_**(i.e., it contains exactly one "@" symbol and at least one "." after the "@").**_

<details>

<summary>Solution</summary>

```python
email = input("Enter an email address: ")
if email.count("@") == 1 and "." in email[email.index("@"):]:
    print("The email address is valid")
else:
    print("The email address is not valid")
```

</details>

### Questions using if-else ladder and nested if-else

12. **`Write a program to calculate the electricity bill (accept number of unit from user) according to the following criteria :`**

| Unit                  | Price                |
| --------------------- | -------------------- |
| **`First 100 Units`** | **`No charge`**      |
| **`Next 100 Units`**  | **`5 Rs Per Unit`**  |
| **`After 200 Units`** | **`10 Rs Per Unit`** |

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

<mark style="color:green;">**`no_of_unit = int(input('Units : '))`**</mark>

<mark style="color:green;">**`if(no_of_unit<=100):`**</mark>

<mark style="color:green;">**`bill = 0`**</mark>

<mark style="color:green;">**`elif(no_of_unit>100 and no_of_unit<=200):`**</mark>

<mark style="color:green;">**`bill = (no_of_unit-100) * 5`**</mark>

<mark style="color:green;">**`else:`**</mark>

<mark style="color:green;">**`bill = 500 + (no_of_unit - 200)*10`**</mark>

<mark style="color:green;">**`print(bill)`**</mark>

</details>

13. **`Write a program to accept percentage from the user and display the grade according to the following criteria:`**

| Mark               | Grade   |
| ------------------ | ------- |
| **`>=90`**         | **`A`** |
| **`>=80 and <90`** | **`B`** |
| **`>=60 and <80`** | **`C`** |
| **`<60`**          | **`D`** |

{% tabs %}
{% tab title="Example" %}
**`Enter the marks : 87`**

**`B`**
{% endtab %}
{% endtabs %}

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

<mark style="color:green;">**`marks = int(input('Enter the marks : '))`**</mark>

<mark style="color:green;">**`if(marks>=90):`**</mark>

<mark style="color:green;">**`print('A')`**</mark>

<mark style="color:green;">**`elif(marks>=80 and marks<90):`**</mark>

<mark style="color:green;">**`print('B')`**</mark>

<mark style="color:green;">**`elif(marks>=60 and marks<80):`**</mark>

<mark style="color:green;">**`print('C')`**</mark>

<mark style="color:green;">**`else:`**</mark>

<mark style="color:green;">**`print('D')`**</mark>

</details>

14. Write a python program that will check for the following conditions:

· If the light is <mark style="color:green;">green</mark> – Car is allowed to go

· If the light is <mark style="color:yellow;">yellow</mark> – Car has to wait

· If the light is <mark style="color:red;">red</mark> – Car has to stop

· Other signal – unrecognized signal. Example black, blue, etc…

<details>

<summary>Solution</summary>

```python
light = input('Enter Traffic Light : ').lower()
if light == 'green':
    print('Car is allowed to go')
elif light == 'yellow':
    print('Car has to wait')
elif light == 'red':
    print('Car has to stop')
else:
    print(f'unrecognized signal {light}')
```

</details>

15. Write a program to check whether the given number is positive, zero or negative.

<details>

<summary>Solution</summary>

```python
num = int(input('Enter number : '))
if num <0:
    print('Negative')
elif num == 0:
    print('Zero')
else:
    print('Positive')
```

</details>

16. Calculate income tax for the given income by adhering to the below rules

**Taxable Income Rate (in %)**

First Rs.10,0000 0

Next Rs. 10,0000 10

The remaining 20

17. Write a program to take a digit and print it is In words(_**only 0 - 9**_)\
    **For Example :** enter digit : 5\
    Five

<details>

<summary>Solution</summary>

```python
digit = int(input('Enter Digit : '))
if digit >=0 and digit <= 9:
    if digit == 0:
        print('Zero')
    elif digit == 1:
        print('One')
    elif digit == 2:
        print('Two')
    elif digit == 3:
        print('Three')
    elif digit == 4:
        print('Four')
    elif digit == 5:
        print('Five')
    elif digit == 6:
        print('Six')
    elif digit == 7:
        print('Seven')
    elif digit == 8:
        print('Eight')
    elif digit == 9:
        print('Nine')
else:
    print('Digit is either less than 0 and greater than 9')

```

</details>

18. Write a menu driven program for making a simple calculator.

<details>

<summary>Solution</summary>

```python
print("Menu:")
print("1. Add")
print("2. Subtract")
print("3. Multiply")
print("4. Divide")

choice = int(input("Enter your choice (1-4): "))

num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

if choice == 1:
    result = num1 + num2
    print("Result:", result)
elif choice == 2:
    result = num1 - num2
    print("Result:", result)
elif choice == 3:
    result = num1 * num2
    print("Result:", result)
elif choice == 4:
    if num2 == 0:
        print("Error: division by zero")
    else:
        result = num1 / num2
        print("Result:", result)
else:
    print("Invalid choice")

```

</details>

19. An institution has decided to admit new candidates in different streams on the following criteria:

**Total Marks Obtained Streams Offered**

300 and above Science\
200 and above but less than 300 Commerce\
Below 200 but not below 75 Arts\
Otherwise Admission is not granted,\
You have to appear in qualifying examination

Write a program to input total marks obtained in an examination and print the stream allotted on the basis of above criteria.

<details>

<summary>Solution</summary>

```python
marks = int(input("Enter total marks obtained: "))

if marks >= 300:
    stream = "Science"
elif marks >= 200 and marks < 300:
    stream = "Commerce"
elif marks >= 75 and marks < 200:
    stream = "Arts"
else:
    stream = "Qualifying examination"

print("Stream allotted: ", stream)

```

</details>

20. Design a Program to input two integers **num1, num2** and a **character(opr)**. The Variable **opr** reads only one of the four `characters(+,-,/,*)`. Your Program should perform the operation on the basis of **`operator on num1, num2`**. _In case of subtraction, subtract smaller number from bigger number and in case of division divide the greater number by smaller numbers._\
    \
    &#xNAN;_&#x50;rint Integers and result._
21. A Scooter /motor cycle stand charges the following rates for the parking:

**Hours Rate**

First 4hours RS.5.00\
Every next hour upto5 hours RS.3.00 per hour\
Any further hour above 9 hour RS.2.00 per hour

Write a program to input the number of **hours** for which a two wheeler is parked. Calculate and print the parking charges to be paid by the customer.

22. Monthly Electricity bill is calculated as –

**Number of units Consumed Rate Per Unit**

<=100 only meter rent Rs 200/-\
For next 200 units Rs. 1.00 per unit\
For next 200 units Rs 1.55 per unit\
For more than 500 units Rs 2.10 per unit

Write a program to take the **consumer number, number of units consumed**. _Calculate bill amount_. Print consumer number and total amount to be paid by the consumer. (_Consumer number must be digits of length 5 and print appropriate message for incorrect input of consumer number_).

<details>

<summary>Solution</summary>

```python
consumer_number = input("Enter consumer number (5 digits): ")
if not consumer_number.isdigit() or len(consumer_number) != 5:
    print("Invalid consumer number!")
else:
    units_consumed = int(input("Enter number of units consumed: "))
    if units_consumed <= 100:
        total_amount = 200
    elif units_consumed <= 300:
        total_amount = 200 + (units_consumed - 100) * 1.00
    elif units_consumed <= 500:
        total_amount = 200 + 200 * 1.00 + (units_consumed - 300) * 1.55
    else:
        total_amount = 200 + 200 * 1.00 + 200 * 1.55 + (units_consumed - 500) * 2.10
    print("Consumer number:", consumer_number)
    print("Total amount to be paid:", total_amount)

```

</details>

23. Write a menu driven program for three options. (_Take input of option from user_).

i) Area of circle\
ii) Area of Rectangle\
iii) Area of Square

Print the area along with sides.

24. A Bank offers the following rate of interest for fixed deposit:

**Time(Years) Rate(%)**

<1 9.0\
1 to 2 10.0\
2 to 3 11.0\
\>3 12.0

The amount A after n years is calculated by using the formula:\
**A = P(1 + r / 100)^n**

Where P = principal amount deposited\
R = rate of interest\
N = number of years

Write a program to accept the deposited amount, number of years the amount is to be deposited for n and compute accrued amount for an investor.

<details>

<summary>Solution</summary>

```python
p = float(input("Enter the principal amount: "))
n = float(input("Enter the number of years: "))

if n < 1:
    rate = 9.0
elif 1 <= n <= 2:
    rate = 10.0
elif 2 < n <= 3:
    rate = 11.0
else:
    rate = 12.0

amount = p * (1 + rate/100)**n

print("Principal amount: Rs.", p)
print("Rate of interest: ", r, "%")
print("Number of years: ", n)
print("Amount: Rs.", amount)

```

</details>

25. Write a program to take number input between 1 to 7 and print the day associated to that number such as 1 for Sunday, 2 for Monday, etc.

<details>

<summary>Solution</summary>

```python
day_number = int(input('Enter Day Number : '))

if day_number >= 1 and day_number <= 7:
    if day_number == 1:
        print('Sunday')
    elif day_number == 2:
        print('Monday')
    elif day_number == 3:
        print('Tuesday')
    elif day_number == 4:
        print('Wednesday')
    elif day_number == 5:
        print('Thursday')
    elif day_number == 6:
        print('Friday')
    elif day_number == 7:
        print('Saturday')
        
else:
    print('Invalid Day Number')

```

</details>

26. Write a program to take number input between 1 and 12 and print the month associated with it.

<details>

<summary>Solution</summary>

```python
month_num = int(input('Enter Month Number : '))

if month_num >= 1 and month_num <= 12:
    if month_num == 1:
        print('January')
    elif month_num == 2:
        print('February')
    elif month_num == 3:
        print('March')
    elif month_num == 4:
        print('April')
    elif month_num == 5:
        print('May')
    elif month_num == 6:
        print('June')
    elif month_num == 7:
        print('July')
    elif month_num == 8:
        print('August')
    elif month_num == 9:
        print('September')
    elif month_num == 10:
        print('October')
    elif month_num == 11:
        print('November')
    elif month_num == 12:
        print('December')
else:
    print('Invalid Month Number')

```

</details>

27. Write a python program to accept the percentage from the user and display the category according to the following criteria:\
    **Percentage Category**

<40 Failed\
\>=40 and <55 Fair\
\>= 55 and <65 Good\
\>= 65 Excellent

<details>

<summary>Solution</summary>

```python
# take input from user
percentage = float(input("Enter the percentage: "))

# check the category based on the percentage
if percentage < 40:
    print("Failed")
elif percentage >= 40 and percentage < 55:
    print("Fair")
elif percentage >= 55 and percentage < 65:
    print("Good")
else:
    print("Excellent")

```

</details>

28. Take three sides (number) from the user and tell whether the triangle is isosceles, scalene and equilateral triangle.

<details>

<summary>Solution</summary>

```python
# take input from user
a = float(input("Enter the length of side a: "))
b = float(input("Enter the length of side b: "))
c = float(input("Enter the length of side c: "))

# check if it forms a triangle
if a + b > c and a + c > b and b + c > a:
    # check for equilateral triangle
    if a == b == c:
        print("The triangle is an equilateral triangle.")
    # check for isosceles triangle
    elif a == b or b == c or a == c:
        print("The triangle is an isosceles triangle.")
    # otherwise, it must be a scalene triangle
    else:
        print("The triangle is a scalene triangle.")
else:
    print("These sides do not form a triangle.")

```

</details>

29. Alice, Bob and Charlie are bidding on an artifact at an auction.

Alice bids A rupees, Bob bids B rupees and Charlie bids C rupees (where A, B and C are distinct).

According to the rule of the auction, the one who bids the highest amount will win the auction. Determine who will win the auction.

**Input:**

Take input of alice, bob and Charlie’s amount.

**Output:**

Print the name of auctioner who wins the auction.

<details>

<summary>Solution</summary>

```python
# take input from user
a = float(input("Enter Alice's bid: "))
b = float(input("Enter Bob's bid: "))
c = float(input("Enter Charlie's bid: "))

# check who has the highest bid
if a > b and a > c:
    print("Alice wins the auction!")
elif b > a and b > c:
    print("Bob wins the auction!")
elif c > a and c > b:
    print("Charlie wins the auction!")
else:
    print("There is no clear winner. Two or more people have bid the same highest amount.")
#else condition have been added despite of A,B and C
#being distinct as specified by question
#but it is just for clear understanding of the program.
```

</details>
