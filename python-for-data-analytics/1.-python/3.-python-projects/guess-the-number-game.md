# Guess the Number Game

### **Create a game called 'Guess the number'. Let us go through the Rules one by one.**

**1. The computer will generate a Random Number.**

**2. Ask the user to guess the number in 10 chances.**

**3. If the user guesses it right, Score him accordingly like if the user guesses in the first chance, the score is 100, in second chance score should be 90, and so on.**

4. **If the guess number is greater than the random number give him 'Hint: Choose a Lower Number' or less than the random number give him 'hint: Choose a Higher Number' or if the guess number is equal to random, No need to hint, just display score and end the game.**

**5. Also show how many chances are left.**

**6. if the user cannot guess the number, disclose the random number and end the game.**

<details>

<summary>Example</summary>

**`Guess the number : 60`**

**`Hint : Choose a Lower Number`**

**`---------------Number of Chances Left -------------->1`**

**`Guess the number : 50`**

**`Hint : Choose a Higher Number.`**

**`---------------Number of Chances Left -------------->2`**

**`Guess the number : 55`**

**`Hint : Choose a Higher Number.`**

**`---------------Number of Chances Left -------------->3`**

**`Guess the number : 58`**

**`You Won .`**

**`Score : 70`**

</details>

<details>

<summary>Solution</summary>

```python
import random
random_number = random.randint(1,100) 
print(random_number)
chances = 1 
score = 110 
while(chances<=10): 
    guess_number = int(input('Guess the number : ')) 
    if(guess_number==random_number): 
        score = score - chances*10 
        print(f'You Won . Score : {score}') 
        break 
elif(guess_number>random_number): 
    print('Hint : Choose a Lower Number') 
else: 
    print('Hint : Choose a Higher Number.') 
    print(f'---------------Number of Chances Left -------->{chances}') 
    chances = chances + 1 
else: 
    print(f'Sorry ! You lost . You ran out of your chances. Random number was : {random_number}')
```

</details>
