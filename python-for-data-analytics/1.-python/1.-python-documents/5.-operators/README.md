# 5. Operators

{% embed url="https://youtu.be/Yu1i41wU2sg" %}

### **What are Operators?**

Operators are symbols, that are used to perform operations on Operands (**Variables** and **Values.**) There are variety of Operators which are as follows:<br>

* Arithmetic operators
* Assignment operators
* Comparison Operators
* Logical Operators

### 1. Arithematic Operators (+, -, \*, /, \*\*, //, %)

Arithmetic operators are used to perform mathematical operations between two Variables or Values. There are various arithmetical operators that we can use in Python, as follows:

### a. Addition by +:

$$+$$ is used to add two operands (Variables or Values). \
For example:

```
first_number = 30
second_number = 20
result = first_number + second_number
print(result)
```

```
50
```

**Note: In the case of string data, a string can be added with a string value, and as a result, the characters get merged(not allowed with an integer or float value).**

```
first_name='ayush'
last_name='mishra'
full_name=first_name + last_name
print(full_name)
```

```
ayushmishra
```

### b. Multiplication by $$∗$$:

$$∗$$ is used to perform multiplication of two operands (Variables or Values). \
For Example:

```
first_number = 30
second_number = 20
result = first_number * second_number
print(result)
```

```
600
```

**Note: In the case of string data, a string can be multiplied by an integer value, and as a result, the characters get repeated depending upon the integer value(not allowed with a float value).**

```
company='console'
result= company * 3
print(result)
```

```
consoleconsoleconsole
```

### c. Exponent(raised to the power) by $$∗∗$$:

$$∗∗$$ means to the power of. It is used to raise the number on the left to the power of the exponent on the right. That is, in the expression 5 \*\* 3, 5 is being raised to the 3rd power, which is 125. For example:

```
base = 10
power = 2
result = base ** power            # 10*10
print(result)
```

```
100
```

### d. Division by $$/$$:

$$/$$ performs division between two Operands. It always gives **Quotient as** output in the float data type(always). \
For example:

```
first_number = 10
second_number = 5
result = first_number / second_number
print(result)
```

```
2.0
```



### e. Floor Division by $$//$$:

$$//$$ performs division between two operands. It always gives **Quotient** as output. It always gives output in the Integer data type.&#x20;

For example:

```
first_number = 5
second_number = 2
result = first_number // second_number
print(result)
```

```
2
```

### f. Modulus by % :

% performs division between two operands. It always gives the **Remainder** as output. The output comes in an Integer data type.&#x20;

For example:

```
first_number = 5
second_number = 2
result = first_number % second_number
print(result)
```

```
1
```

Example 2:

```
num1= 56
num2= 23
print(num1/ num2)
print(num1 // num2)
print(num1 % num2)
```

```
2.4347826086956523
2
10
```

### 2.  Assignment Operators: $$=,+=,−=,∗=,/=,∗∗=,//=$$

The Assignment Operators are used to assign the value from the right expression to the left variable.

**a**. $$=$$: It assigns the value on the right side to the variable on the left.

For example:

```
a = 5
print(a)
```

```
5
```

**Note: Do not get Confused.** = and == are both different operators. $$=$$ is an assignment operator, while == is a comparison operator (compares if the two values are equal or not).

**b**. $$+=$$ :  We have often used expressions like a = a+5, which will add 5 to the previous value of a and then assign it to a. We can simply write this expression as a+=5.

For example:

```
x = 5 
x = x+5
print(x)
```

```
10
```

We can write x = x + 5 as x+=5.

In \[7]:

```
x = 5
x+=5
print(x)
```

```
10
```

**Note:** $$+=$$ performs operation on same variable and store value in the same variable. This is how rest assignment operators($$−=,∗=,/=,∗∗=,//=$$−=,∗=,/=,∗∗=,//=,%=) in Python work.

### 3. Comparison Operators: $$>,<,>=,<=,!=,==$$

Comparison operators are used to compare two operands and give Boolean True or False values accordingly, as follows:

### a. Greater than by > :

$$>$$ If the left operand is greater than the right operand, then the output comes becomes True; otherwise False. For Example:

```
num1= 7
num2= 3
result= num1 > num2
print(result)
```

```
True
```

### b. Smaller than by < :

$$<$$ If the left operand is less than the right operand, then the output becomes True; otherwise, False.&#x20;

For Example:

```
x = 3
y = 5
output = x<y
print(output)
```

```
True
```

### c. Equals to by $$==$$ :

$$==$$ If the value of two operands is equal, then the condition becomes True; otherwise, False.

For Example:

```
x = 3
y = 5
output = x==y
print(output)
```

```
False
```

### d. Greater than or equal to by >= :

$$>=$$ Checks if the left operand is either greater than or **equal to** the right operand, then the output becomes True, otherwise False.&#x20;

For Example:

```
x = 5
y = 5
print(x>=y)
```

```
True
```

### e. Smaller than or equal to by <= :

$$<=$$ Checks if the left operand is either less than o**r equal to** the right operand, then the condition becomes True, otherwise False.&#x20;

For Example:

```
x = 3
y = 5
output = x<=y
print(output)
```

```
True
```

### f. Not Equals to by $$!=$$ :

$$!=$$ Make sure that if the value of the two operands must not be equal, then the output becomes True; otherwise, False.

For Example:

```
x = 3
y = 5
out = x!=y
print(out)
```

```
True
```

{% embed url="https://youtu.be/d2vo5-kE7Mw" %}

### 4.Logical Operators:$$and$$, $$or$$ , $$not$$

The concept of logical operators is simple. They allow a program to make a decision based on multiple conditions.They return output in boolean i.e. True or False.

$$and$$: If both expressions are True , Output will be True otherwise False.For Example:

In \[8]:

```
x = 7>3 and 4>3
print(x)
y = 7>3 and 5>9
print(y)
```

```
True
False
```

$$or$$ : If atleast one expression is True , Output will be True otherwise False.For Example:

In \[10]:

```
x = 7>3 or 4>3
print(x)
y = 7>3 or 5>9
print(y)
z=7<3 and 5<4
print(z)
```

```
True
True
False
```

$$not$$ : If expression is True , Output will be False and vice-versa.For Example:

In \[11]:

```
x = 5>3
not(x)
```

Out\[11]:

```
False
```

### Operator Precedence (Priority Of Operators):

**What is Operator Precedence?**

To understand Operator Precedence better , let's start with an example:

In \[ ]:

```
x = 2
y = 2
z = 2
p = 2
calc = x-y*p**z
print(calc)
```

What do you think output of this **calc** would be? This may be confusing as we don't know which operator will be solved at first.

Operator Precedence is known as Priority of Operators, which will tell us which operator will be solved at first.

In the above example, power has higher priority than multiplication and multiplication has higher priority than addition. So the output would be : -6. let' see:

In \[12]:

```
x = 2
y = 2
z = 2
p = 2
calc = x-y*p**z
print(calc)
```

```
-6
```

Priority Table of Python :

$$()−Parentheses$$

$$∗∗−Exponent$$

$$∗,/,//$$,% $$Multiplication,Division,Floordivision,Modulus$$

$$+,−$$ $$Addition,Subtraction$$

$$==,!=,>,>=,<,<=$$ $$Comparisons$$

$$LogicalNOT$$

$$LogicalAND$$

$$LogicalOR$$

**Do Not Confuse:** if you look closely, there are many operators with same priority, so if you come up with expression with same priority operators , you will solve it from left to right. Look at the code below:In \[13]:

```
x = 2
y = 2
z = 2
p = 2
calc = x+y-p/z
print(calc)
```

```
3.0
```

In the Code above firstly $$/$$/ (division Operator) solved , after that from right to left we solved the expression. first $$/$$/ then $$+$$+ then $$−$$−

In \[ ]:

```
 
```

### Assignment:

* Make a calulator like program where it perform additions, multiplication, division,subtraction on two values.
* Take two variables and divide one with another in such a way that the quotient comes as output.
* What will be the output of following program:

In \[ ]:

```
a = False
b = False
x = not(a)
y = not(b)
print(a and b)
print(a and x)
print(y and b)
print(x and y)
```

* Write a Program where output is value raised to the power 100.
