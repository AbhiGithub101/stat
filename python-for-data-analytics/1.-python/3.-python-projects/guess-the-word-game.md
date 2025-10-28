# Guess the Word Game

## Guess the Word Game

**Python is a powerful multi-purpose programming language used by multiple giant companies. It has simple and easy-to-use syntax making it the perfect language for someone trying to learn computer programming for the first time.**

**In this Project, You have been provided to create a guess the word game which will choose a secret or magic word and ask the user to guess the word by providing the letters.**

**These letters provided must automatically be placed at the position where they are in the word so that user may understand and guess the magic word.**

Your Program must provide 10 options to a user to guess and win the game.

Print the Appropriate Messages for clear understanding of the game.

**Prerequisite**

Python - Basic concepts

Random Module

{% tabs %}
{% tab title="Example 1" %}
This time the word is **SNAKE**

```
--------Guess the Word Game---------------
You Have 10 chances to win the game
You have to guess the secret word using letters
The letters will be placed automatically on the place if correct
Let's Start----->
_ _ _ _ _ 
Enter the character : o
_ _ _ _ _ 

Try Again!!
Enter the character : m
_ _ _ _ _ 

Try Again!!
Enter the character : a
_ _ a _ _ 

Try Again!!
Enter the character : n
_ n a _ _ 

Try Again!!
Enter the character : s
s n a _ _ 

Try Again!!
Enter the character : k
s n a k _ 

Try Again!!
Enter the character : e
s n a k e 

s n a k e 
You Won the Game
------------------------------------------
```
{% endtab %}

{% tab title="Example 2" %}
In this Guess may be wrong.

```
--------Guess the Word Game---------------
You Have 10 chances to win the game
You have to guess the secret word using letters
The letters will be placed automatically on the place if correct
Let's Start----->
_ _ _ _ _ 
Enter the character : n
_ _ _ _ _ 

Try Again!!
Enter the character : h
_ _ _ _ _ 

Try Again!!
Enter the character : a
_ _ _ a _ 

Try Again!!
Enter the character : e
_ _ e a _ 

Try Again!!
Enter the character : l
_ _ e a _ 

Try Again!!
Enter the character : s
_ _ e a _ 

Try Again!!
Enter the character : n
_ _ e a _ 

Try Again!!
Enter the character : m
_ _ e a _ 

Try Again!!
Enter the character : r
_ r e a _ 

Try Again!!
Enter the character : b
b r e a _ 

Try Again!!
You Lose the Game
----------------------------------------------
```
{% endtab %}
{% endtabs %}

<details>

<summary>Solution</summary>

```python
import random as rd

#List of words for guessing
words = ['SEVEN', 'SNAKE', 'APPLE', 'MANGO', 'TOMB', 'JERRY', 'HELLO'\
         , 'HAPPY', 'BREAK']

#function for printing _ _ _ _ _ and words on the right place
def print_place(lst):
    for i in lst:
        print(i, end=' ')
    print()


#Printing the game instruction
print('--------Guess the Word Game---------------')
print('You Have 10 chances to win the game')
print('You have to guess the secret word using letters')
print('The letters will be placed automatically on the place if correct')
print("Let's Start----->")

#selecting the word from the list of words
word = rd.choice(words)

#creation of a list for placing _ _ _ _ _
lst = ['_' for i in range(5)]

#Printing the first time
print_place(lst)
win = False
#running the loop for executing the game with 5 chances.
for i in range(10):
    char = input('Enter the character : ')
    for i in range(5):
        if word.lower()[i] == char:
            lst[i] = char

    print_place(lst)
    print()
    if "".join(lst) == word.lower():
        print_place(lst)
        win = True
        print('You Won the Game')
        print('------------------------------------------')
        break
    else:
        print('Try Again!!')            

if not win:
    print('You Lose the Game')
    print('----------------------------------------------')

```

</details>
