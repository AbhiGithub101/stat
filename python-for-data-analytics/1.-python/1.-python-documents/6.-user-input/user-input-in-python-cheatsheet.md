# User Input In Python CheatSheet

## User Input In Python <a href="#user-input-in-python" id="user-input-in-python"></a>

input() function is used to get input from the user. It always takes data as a string. No calculations are done at the input level.

```
#1. Input Without Message--> Used when instructions are already printed.

value = input()
print(value)
```

```
#2. Input with Message--> We can also give an appropriate message to the user, to let the user know that what type of data he/she needs to enter.

# Example 1--> Taking city_name from user as input
city = input("Enter your city: ")  # Input: Delhi
print("I live in city:", city)  # Output: I live in Delhi

# Example 2--> Taking name from the user as input
name = input("Enter your name: ")  # Input: Aman Gaur
print(name)  # Output: Aman Gaur
```

```
#3. User Input in Print Formatting--> We can also display our data by using string formatting.

name = input("Enter name: ") # Input: Ayush Mishra
city = input("Enter your city: ") # Input: Noida
age= input("Enter your age: ") # Input: 89
print(f'My name is {name}, I am {age} years old and my city is {city}') # My name is Ayush Mishra , I am 89 years old and my city is Noida
```
