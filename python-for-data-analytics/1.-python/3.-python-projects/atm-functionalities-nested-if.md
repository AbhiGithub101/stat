---
description: >-
  In this project we will create a program which shows how an atm machine works
  related to basic functions as show account balance,cash withdraw,cash deposit
  and pin change.
---

# Atm-functionalities(nested if)

firstly, we will declare 3 variables. one for account balance, one for an account number, and one for the pin, and initialize those variables

```
pin='1234'
account_balance=50000
account_number=4567893210
```

Now we will create a display screen of the atm along with a menu that will guide the user on the facilities a user can use from the machine.

```
print('Welcome to XYZ atm')
print('''1. Show account balance.
2. Cash withdrawal
3. Cash deposit
4. Pin Change''')

ch=input('enter your choice:')
```

Now we will code for the 1st option i.e. if the user selects Show Account Balance

```python
if ch=='1':
    x=input('enter your pin:')
    if pin==x:
        print(f'you have {account_balance} in your account.')
    else:
        print('you have entered wrong pin.')
```

Now we will code for the 2nd option i.e. if the user selects for Cash Withdrawal.

```python
elif ch=='2':
    cash_withdrawal=int(input('enter the amount you wish to withdraw:'))
    x=input('enter your pin:')
    if pin==x:
        if cash_withdrawal<=account_balance:
            print(f'collect you cash')
        else:
            print('you do not sufficient funds')
    else:
        print('you have entered wrong pin')
        
```

Now we will code for the 3rd option i.e. if the user selects for Cash Deposit.

```python
elif ch=='3':
    account_details=input('enter the account details:')
    if account_details==account_number:
        n2000=int(input('Enter the number of 2000 Rs notes:')
        n500=int(input('Enter the number of 500 Rs notes:')
        n200=int(input('Enter the number of 200 Rs notes:')
        n100=int(input('Enter the number of 100 Rs notes:')
        cash_deposit=(n2000*2000) + (n500*500) + (n200*200) + (n100*100)
        print(f' you have deposited Rs. {cash_deposit} in your account')
    else:
        print('you have entered wrong account number')
```

Now we will code for the 4th option i.e. Pin Change.

```python
elif ch=='4':
    x=input('enter your pin:')
    if pin==x:
        n_pin=input('enter new pin:')
        re_n_pin=input('re enter new pin:') 
        if n_pin==re_n_pin:
            pin=pin.replace(n_pin,pin)
            print('you have successfully changed your pin')
        else:
            print('pins do not match')
    else:
        print('you have entered wrong pin')
```

If the user selects any option other than (1-4).code

```python
else:
    print('you have entered wrong option')
```

Practice this project yourself and try to create the next project on your own.

### The KBC Game

1. Create a virtual environment for the user by displaying the message ''Welcome to The KBC Game."
2. Display rules of the game:\
   Rules:\
   1\. You will be asked 5 questions from general knowledge.\
   2\. You have to select your answer from the 4 options provided.\
   3\. For every correct answer you will be awarded 1000 Rs.\
   4\. In case of a wrong answer, you will be penalized by 500 Rs.
3. You have to create a quiz game program where the system asks 5 questions from the user related to any field and then the user is provided with 4 options. From this, he has to choose 1 option for the correct answer.
4. If the user selects the correct answer, he will be awarded 1000 Rs.
5. For every incorrect answer, the user will be penalized by 500 Rs.
6. At the end of the game, the program must display a message to the user about how many answers were correct and how many were incorrect.
7. Also, show the final amount he won from the game.

