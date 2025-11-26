# Operators Assignment

1. The Output of **a = 2+3-4/2\*\*2** and also tell its type?
   1. 4 and int
   2. 4.0 and float
   3. 1.0 and float
   4. 5 and int

<details>

<summary>Solution</summary>

Answer : option 2

</details>

2\. The output of the following python code snippet\
**print(type(4/2))**\
**print(type(4//2))**

1. float and float
2. float and int
3. int and float
4. int and int

<details>

<summary>Solution</summary>

Answer: option 2

</details>

3. What will be the output of the following python code snippet\
   **a= 12**\
   **print(type(a))**\
   **a=’12345’**\
   **print(type(a))**

a. Int and str\
b. Int and int\
c. str and int\
d. str and str

<details>

<summary>Solution</summary>

Answer: option **a**

</details>

4. In which manner are operators with the same precedence evaluated?

a. Left to right\
b. Right to left\
c. Can’t say\
d. None of the Above Mentioned

<details>

<summary>Solution</summary>

Answer: option **a**

</details>

5. Output of _**a = 2\*3/4\*\*1==2.00**_

a. 1.5\
b. 2\
c. True\
d. False

<details>

<summary>Solution</summary>

Answer: option **d**

</details>

6. Output of the following\
   **print(100>2 and 100 > 30)**

a. True\
b. False\
c. 100\
d. 30

<details>

<summary>Solution</summary>

Answer: option **a**

</details>

7. What will be the output of the following code\
   \
   **print(True or True and False)**

a. True\
b. False

<details>

<summary>Solution</summary>

Answer : _**a**_ because **and** has higher precedence over **or**

</details>

8. What will be the precedence of

**a. Not**\
**b. And**\
**c. Or**

a. Abc\
b. Bac\
c. Bca\
d. Cab

<details>

<summary>Solution</summary>

Answer: a

</details>

9. The Output of the following **2/2\*3\*\*2<=10**

a. True\
b. False\
c. 9\
d. 10

<details>

<summary>Solution</summary>

Answer : a

</details>

10. **type(22%3) = ?**

a. Int\
b. Str\
c. Float\
d. Can’t say

<details>

<summary>Solution</summary>

Answer: **a**

</details>

11. Which of the following code is correct in Python?

a. A++\
b. ++a\
c. A += 1\
d. Both A and B

<details>

<summary>Solution</summary>

Answer: **d**

</details>

12. Suppose, there are 5 rupees in your pocket.

* I am giving you 17 Rs. How many rupees do you have now?
* Now I am giving you 39 Rs. How many rupees do you have now?
* Now I am taking 23 Rs. back. How many rupees do you have now?
* Again I am giving you 932 Rs. How many rupees do you have now?

<details>

<summary>Solution</summary>

```python
a=5
a=a+17              # I am giving you 17 Rs.
print(a)            # How many rupees do you have now?

a=a+39      # I am giving you 39 Rs.
print(a)    # How many rupees do you have now?

a=a-23      # I am taking 23 Rs. back.
print(a)    # How many rupees do you have now?

a=a+932     # I am giving you 932 Rs.
print(a)    # How many rupees do you have now?
```

</details>

13. Calculate the value of ( a ) in the expression: a =( 5 + 3 - 2 / 2 ).

<details>

<summary>Solution</summary>

7.0

</details>

14. Calculate the value of ( b ) in the expression: b = ((8 - 2) \* 3 / 2 )

<details>

<summary>Solution</summary>

9.0

</details>

15. Calculate the value of ( c ) in the expression: c =( 10 / 2 + 3 \* 4 )

<details>

<summary>Solution</summary>

17.0

</details>

16. Calculate the value of ( d ) in the expression: d =( 7 + 3 \* (2 \*\* 2) - 5 )

<details>

<summary>Solution</summary>

14

</details>

17. Calculate the value of ( e ) in the expression: e =( (6 / 3) + (8 - 4) )

<details>

<summary>Solution</summary>

6.0

</details>

18. Calculate the value of ( f ) in the expression: f = (5 \* (3 + 2) - 8 / 4 )

<details>

<summary>Solution</summary>

23.0

</details>

19. Calculate the value of ( g ) in the expression: g =( 12 / 4 + 7 - 3 \* 2 )

<details>

<summary>Solution</summary>

4.0

</details>

20. Calculate the value of ( h ) in the expression: h = (9 - 3 + 4 \* (2 \*\* 2) )

<details>

<summary>Solution</summary>

22

</details>

21. Suppose, you have 150 rupees.

* [ ] You spend 45 rupees on a meal. How many rupees do you have now?
* [ ] Then, you spend 32 rupees on a movie ticket. How many rupees do you have now?
* [ ] Next, you spend 18 rupees on snacks. How many rupees do you have now?
* [ ] Finally, you spend 25 rupees on transportation. How many rupees do you have now?

<details>

<summary>Solution</summary>

```python
# Initial amount
rupees = 150

# Spending amounts
rupees -= 45  # spend on meal
print(rupees)
rupees -= 32  # spend on movie ticket
print(rupees)
rupees -= 18  # spend on snacks
print(rupees)
rupees -= 25  # spend on transportation


# Final amount
print(rupees)

```

</details>

22. You have 200 rupees.

* [ ] You decide to buy a book for 60 rupees. How much do you have left?
* [ ] Then, you receive 30 rupees from a friend. How much do you have now?
* [ ] You decide to donate 10% of your current money to charity. How much do you have left?
* [ ] You find 5 rupees in your pocket. Add this to your current amount.
* [ ] You want to split the remaining amount equally between yourself and a friend. How much does each of you get?
* [ ] You win a prize and the amount you have is tripled. How much do you have now?
* [ ] Finally, you purchase a rose, usually the price of rose is 50 rupees but todaythe price is incremented by 10 rupees due to demand. How much do you pay now?

<details>

<summary>Solution</summary>

```python
# Initial amount
amount = 200

# Step 1: You buy a book for 60 rupees
amount -= 60
print('Money left:',amount)

# Step 2: You receive 30 rupees from a friend
amount += 30
print('Money left:',amount)

# Step 3: You donate 10% of your current money to charity
charity_amount= amount * 10/100
amount -=charity_amount
print('Money left:',amount)

# Step 4: You find 5 rupees in your pocket
amount += 5
print('Money left:',amount)

# Step 5: You split the remaining amount equally with a friend
amount /= 2
print('Money left:',amount)

# Step 6: Your amount is tripled as you win a prize
amount *= 3
print('Money left:',amount)

# step 7: price of rose is 50 but increased by 10 rupees.

rose_price=50
rose_price+=10
print('rose price paid:',rose_price)
amount-= rose_price
print('Money left:',amount)


```

</details>
