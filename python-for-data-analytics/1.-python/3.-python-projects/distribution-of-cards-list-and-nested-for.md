---
description: >-
  We are going to create a program that will distribute 52 cards of a deck
  amongst 4 players "Randomly".
---

# Distribution of Cards(List & Nested for)

## Distribution of Cards(List & Nested for)

Before creating a program we have to create those cards in Python language.\
In a deck of cards, there is a collection of 52 cards categorized into 2 types (numbers and suits(houses)).\
numbers= \['Ace', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'Jack', 'Queen', 'King']\
suits= \['Hearts', 'Diamonds', 'Clubs', 'Spades']\
The cards we are going to create will be in the form of tuple\
ex:: ('Ace','club'),('king','spades'),('10',' hearts),('5','diamonds')

1. In this program, we are going to import a random library so that we can use the shuffle() function to generate randomness in the cards.co

```
import random
```

2. Now we are going to create a deck of 52 cards. For that, we have to take 2 lists.\
   1st list includes number cards.\
   2nd list includes suits

```
suits = ['Hearts', 'Diamonds', 'Clubs', 'Spades']
ranks = ['Ace', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'Jack', 'Queen', 'King']

```

3. Now that we have created the lists. It's time to combine them, make cards, and then form a deck.

```
deck=[]
for suit in suits:
    for rank in ranks:
      deck.append((rank,suit))
```

4. Now is the time to shuffle the deck before the distribution of cards. For that, we will use the shuffle() function of the random library.

```
random.shuffle(deck)
```

5. Now we have to code to create a game that consists of 4 players and we will divide the cards amongst them to start the game.

```
game=[]
for i in range(4):
    l=[]
    player=input(f'enter the name of {i} player:')
    for card in deck[i::4]:
        l.append(card)
    l.insert(0,player)
    game.append(l)

```

6. Now the distribution is completed, random, and equal. we can check the cards of the player (optional) and start the game.

```
for i in game:        # OPTIONAL
    print(i)          # OPTIONAL
print('LET THE GAME BEGINS')
```
