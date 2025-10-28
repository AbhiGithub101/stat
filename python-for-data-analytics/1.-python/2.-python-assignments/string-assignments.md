# String Assignments

1. _**`String is a Collection of __________`**_

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

**Characters**

</details>

2\. _**`Strings are enclosed within _________`**_

* _**`Single Quotes (' ')`**_
* _**`Double Quotes (" ")`**_
* _**`Triple Quotes (''' ''' or """ """)`**_
* _**`Any of the Above`**_

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

**Any of the above**

</details>

_3._ Ask the user to enter their name and display it in reverse order (last name first).

Sample Input: Ayush Mishra\
Sample Output: Mishra Ayush

<details>

<summary>Solution</summary>

```python
name=input('Enter your name:')
name=name.split(' ')
rev_name=name[-1] + name[0]
print(f'Reversed Name:{rev_name}')
```

</details>

4. Take a word as input from the user and print the first and last character.

<details>

<summary>Solution</summary>

```python
word=input('Enter a word:')
print(f'First character:{word[0]')
print(f'Last character:{word[-1]')
```

</details>

5. _**`What is the Positive and negative index number of space in Word - David Joseph:`**_

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

<mark style="color:green;">**Positve Index number of first letter D starts with 0, hence index number of space will be: 5**</mark>

<mark style="color:green;">**Negative Index number of last letter h is -1, hence index number of space will be: -7**</mark>

**Code :**

<mark style="color:green;">**`name = 'David Joseph'`**</mark>

<mark style="color:green;">**`pi = name.find(' ')`**</mark>

<mark style="color:green;">**`print('Positive index : ',pi)`**</mark>

<mark style="color:green;">**`total_char = len(name)`**</mark>

<mark style="color:green;">**`ni = pi - total_char`**</mark>

<mark style="color:green;">**`print('Negative index : ',ni)`**</mark>

</details>

6. **`How to get the first character in upper case from the name inputted by the User.`**\
   &#xNAN;**`For example :`**\
   &#xNAN;**`name : 'david Joseph'`**\
   &#xNAN;**`Output : D`**

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

**First thing that we need to do , is to take input from user.**

<mark style="color:green;">**`name = input('Enter Your Name : ')`**</mark>

**Now name given by user can be in lower case or in upper case or a mix of it. But we need first character in uppercase, So what method do we use to convert string in Upper case :** [**upper()**](https://training.gitbook.io/python-documents/strings-in-pythn#2.upper-method\\)**.**

<mark style="color:green;">**`result = name[0]`**</mark>

**It will give you first character , but we need to be sure that it is in uppercase. So it is better to assign this value in result.**

<mark style="color:green;">**`result = name[0].upper()`**</mark>

<mark style="color:green;">**`print(f'First Character in String is {result}.')`**</mark>

</details>

7. **`You work in a company and you are given customers number, But many customers filled wrong data, so you need to check if the number given by customer is right or not.`**

**`Phone Number should match following Criteria :`**

1. **`Only numbers , spaces are allowed though (so few customers wrote their number with spaces.)`**
2. **`10 character only.`**

For Example

{% tabs %}
{% tab title="Example 1" %}
`input : 976 543 2319`

**Output :**

`check_number : True`

`ten_character : True`
{% endtab %}

{% tab title="Example 2" %}
`input : 976 543 a319`

**Output :**

`check_number : False`

`ten_character : False`
{% endtab %}
{% endtabs %}

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

**First thing that we need to do is to take input from User.**

<mark style="color:green;">**`number = input('Enter Customer Number : ')`**</mark>

**Now as we know that spaces are allowed, So it is better to replace them with nothing , so that we don't have to worry about them.**

<mark style="color:green;">**`number = number.replace(' ','')`**</mark>

**Now we need to check out first criteria and that is to check if it is number.**

<mark style="color:green;">**`check_number = number.isnumeric()`**</mark>

**Now we need to check our second criteria and that is to check if there are only 10 digits.**

<mark style="color:green;">**`ten_character = len(number)==10`**</mark>

**Voila !!!**

<mark style="color:green;">**`print(f'Check Number : {check_number}')`**</mark>

<mark style="color:green;">**`print(f'Ten character : {ten_character}')`**</mark>

</details>

8. **`Find the second maximum digit from a number`.**

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

**First thing that we need to do is to take input from User.**

<mark style="color:green;">**`number = input('Enter the number : ')`**</mark>

**Now what we need to do is to find the maximum number.**

<mark style="color:green;">**`first_max = max(number)`**</mark>

**Remove this maximum number from the number, so that our second maximum number**

<mark style="color:green;">**`number = number.replace(first_max,'')`**</mark>

**Now that the maximum number is removed from the string, We can find our second maximum number**

<mark style="color:green;">**`second_max = max(number)`**</mark>

<mark style="color:green;">**`print(second_max)`**</mark>

</details>

9. **`You work in a bank, You are tasked to create a pin with the help of their customer name and birthyear .`**

{% tabs %}
{% tab title="Example" %}
**`Input Customer Name : david josh`**

**`Input Date Of Birth : 09-12-1997`**

**`Output:`**

**`pin : David1997`**
{% endtab %}
{% endtabs %}

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

**First we will take inputs from user.**

<mark style="color:green;">**`name = input('Enter Customer Name : ')`**</mark>

<mark style="color:green;">**`dob = input('Enter date of birth : ')`**</mark>

**Now we need to split first name from the user `name` and convert it into title.**

<mark style="color:green;">**`firstname = name.split(' ')[0].title()`**</mark>

**Now we need to get year from User Date of Birth , we can achieve it by splitting last four digits.**

<mark style="color:green;">**`year = dob[-4:]`**</mark>

**Let's concatenate both to get Customer's pin number.**

<mark style="color:green;">**`pin = firstname + year`**</mark>

<mark style="color:green;">**`print(pin)`**</mark>

</details>

10. **`You are tasked to swap first and last characters of a string.`**

`For Example:`

{% tabs %}
{% tab title="Example" %}
**`Input string : 'python'`**

**`Output :`**

**`'nythop'`**
{% endtab %}
{% endtabs %}

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

**First we will take input From user.**

<mark style="color:green;">**`name = input('Enter the string : ')`**</mark>

**We will get First and last character with the help of indexing.**

<mark style="color:green;">**`f = name[0]`**</mark>

<mark style="color:green;">**`l = name[-1]`**</mark>

**Now we need to slice middle string, It means from second character to second last character.**

<mark style="color:green;">**`mid_str = name[1:-1]`**</mark>

**Now you can concatenate in desired order.**

<mark style="color:green;">**`print(l+mid_str+f)`**</mark>

</details>

11. **`Take a String from user consisting only alphabets and spaces, and count How many Consonants and Vowels are in the string.`**

{% tabs %}
{% tab title="Example" %}
**`input string : 'This is example'`**

**`Output :`**

**`Total Alphabets : 13`**

**`Total Vowels : 5`**

**`Total Consonants : 8`**
{% endtab %}
{% endtabs %}

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

```python
#Take a string input from user.
st = input('Enter the string : ').lower()
 
#Now that we do not need spaces , let's remove them for good, by replacing them with empty string.
st = st.replace(' ','') 
#Now only alphabets are in the string , so let us calculate number of alphabets by using len() function.
total_alpha = len(st) 
#Now to count all vowels , we will use count method.
total_vowel = st.count('a')+st.count('e')+st.count('i')+st.count('o')+st.count('u') 
#To count Consonants, all we need to do is to subtract total vowel from total alphabets.
total_cons = total_alpha-total_vowel 
#Voilla !!!
print(total_alpha) 
print(total_vowel) 
print(total_cons)
```

</details>

12. **`Check if a string is palindrome or not. Palindrome is a string that does not change even if you reverse it.`**

For example:

{% tabs %}
{% tab title="Example" %}
**`input string : 'rotator'`**

**`Output:`**

**`Palindrome : True`**

**`input string : 'python'`**

**`Output:`**

**`Palindrome : False`**
{% endtab %}
{% endtabs %}

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

**Let us take an input from user.**

<mark style="color:green;">**`st = input('Enter the string : ')`**</mark>

**Let us reverse the string.**

<mark style="color:green;">**`new_st = st[::-1]`**</mark>

**Now let's compare both strings.**

<mark style="color:green;">**`print(st==new_st)`**</mark>

</details>

13. **`Imagine You run an Institute where all your students are stored in a variable something like this :`**

<mark style="color:green;">**`students = 'david mark bill sam'`**</mark>

**`You have a few tasks to do like :`**

* [x] **Add a student given by user**
* [x] **Delete a student given by user**
* [x] **Check if a student given by user is present or not**
* [x] **Replace a Student given by user**

{% tabs %}
{% tab title="Add a student" %}
<mark style="color:green;">**`students = 'david mark bill sam'`**</mark>

**input :**

**`Enter the name of the student : jeff`**

**`david mark bill sam jeff`**
{% endtab %}

{% tab title="Delete a student" %}
<mark style="color:green;">**`students = 'david mark bill sam'`**</mark>

**input :**

**`Enter the name of the student : sam`**

**`david mark bill`**
{% endtab %}

{% tab title="Find a student" %}
<mark style="color:green;">**`students = 'david mark bill sam'`**</mark>

**input :**

**`Enter the name of the student to find : sam`**

**`True`**
{% endtab %}

{% tab title="Replace a student" %}
<mark style="color:green;">**`students = 'david mark bill sam'`**</mark>

**input :**

**`Enter the name of the old student to replace : sam`**

**`Enter the name of the new student : karen`**

**`david mark bill karen`**
{% endtab %}
{% endtabs %}

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

**So we are given a string for reference; let us use this reference of students to perform such operations.**

<mark style="color:green;">**`students = 'david mark bill sam'`**</mark>

* [x] **Add a student given by user**

<mark style="color:green;">**`student = input('Enter the name of the student : ')`**</mark>

<mark style="color:green;">**`students = students + student`**</mark>

* [x] **Delete a student given by user**

<mark style="color:green;">**`student = input('Enter the name of the student : ')`**</mark>

<mark style="color:green;">**`students = students.replace(student,'')`**</mark>

* [x] **Check if a student given by user is present or not**

<mark style="color:green;">**`student = input('Enter the name of the student : ')`**</mark>

<mark style="color:green;">**`check = student in students`**</mark>

<mark style="color:green;">**`print(check)`**</mark>

* [x] **Replace a Student**

<mark style="color:green;">**`old_student = input('Enter the name of the student to replace : ')`**</mark>

<mark style="color:green;">**`new_student = input('Enter the name of the new student: ')`**</mark>

<mark style="color:green;">**`students = students.replace(old_student,new_student)`**</mark>

<mark style="color:green;">**`print(students)`**</mark>

</details>

14. Find out the name of the company from a URL inputted by the user.\
    Example:\
    url= [www.facebook.com\\](http://www.facebook.com) Output: facebook

<details>

<summary>Solution</summary>

```python
url=input('Enter a url')
url=url.split('.')
company_name=url[1]
print(f'The name of the company is:{company}'
```

</details>

15. Input an email address and extract the username part (before the @).

<details>

<summary>Solution</summary>

```python
email=input('Enter Email ID:')
username= email[0:email.find('@')]
print(f'Your Username:{username}')
```

</details>

16. Take a string input, count the number of vowels and then remove all the vowels.

<details>

<summary>Solution</summary>

```python
str1=input('Enter a string:').lower()
total_vowels= str1.count('a') + str1.count('e') + str1.count('i') + str1.count('o') + str1.count('u')
str1=str1.replace('a','').replace('e','').replace('i','').replace('o','').replace('u','')
```

</details>

17. Ask the user for two strings and check if the second string is a substring of the first.

<details>

<summary>Solution</summary>

```python
str1=input('Enter a sting:')
substr=input('Enter a substring:')

result= substr in str1
print(f'Substring:{result}')
```

</details>

**Which of the following is not a valid string method in Python?**

a) upper()\
b) lower()\
c) title()\
d) subtract()

<details>

<summary>Solution</summary>

Answer: d) subtract()

</details>

**Which of the following code snippets will concatenate two strings in Python?**

a) string1.append(string2)\
b) string1.join(string2)\
c) string1 + string2\
d) string1.concat(string2)

<details>

<summary>Solution</summary>

Answer: c) string1 + string2

</details>

**Which of the following is the correct way to access the first character of a string in Python?**

a) string\[1]\
b) string\[0]\
c) string\[2]\
d) string\[-1]

<details>

<summary>Solution</summary>

Answer: b) string\[0]

</details>

**Which of the following code snippets will reverse a string in Python?**

a) string.reverse()\
b) reversed(string)\
c) string\[::-1]\
d) string.reverse\_string()

<details>

<summary>Solution</summary>

Answer: c) string\[::-1]

</details>

**Which of the following code snippets will return the length of a string in Python?**

a) len(string)\
b) string.length()\
c) string.len()\
d) length(string)

<details>

<summary>Solution</summary>

Answer: a) len(string)

</details>

**Which of the following code snippets will replace all occurrences of a substring in a string in Python?**

a) string.replace(old, new)\
b) string.sub(old, new)\
c) string.replace\_substring(old, new)\
d) string.substitute(old, new)

<details>

<summary>Solution</summary>

Answer: a) string.replace(old, new)

</details>

**Which of the following code snippets will split a string into a list of substrings based on a delimiter in Python?**

a) string.split(delimiter)\
b) string.divide(delimiter)\
c) string.cut(delimiter)\
d) string.separate(delimiter)

<details>

<summary>Solution</summary>

Answer: a) string.split(delimiter)

</details>

**Which of the following code snippets will convert a string to all lowercase letters in Python?**

a) string.lowercase()\
b) string.to\_lower()\
c) string.lower()\
d) string.convert\_to\_lower()

<details>

<summary>Solution</summary>

Answer: c) string.lower()

</details>

**Which of the following code snippets will remove leading and trailing whitespace from a string in Python?**

a) string.strip()\
b) string.trim()\
c) string.remove\_whitespace()\
d) string.trim\_whitespace()

<details>

<summary>Solution</summary>

Answer: a) string.strip()

</details>

**Which of the following code snippets will check if a string starts with a specific substring in Python?**

a) string.check\_start(substring)\
b) string.begins\_with(substring)\
c) string.startswith(substring)\
d) string.starts(substring)

<details>

<summary>Solution</summary>

Answer: c) string.startswith(substring)

</details>

**Which of the following code snippets will split a string into a list of characters in Python?**

a) string.split()\
b) string.chars()\
c) list(string)\
d) string.list()

<details>

<summary>Solution</summary>

Answer: c) list(string)

</details>

**Which of the following code snippets will check if a substring exists in a string in Python?**

a) string.exists(substring)\
b) string.contains(substring)\
c) substring in string\
d) string.sub(substring)

<details>

<summary>Solution</summary>

Answer: c) substring in string

</details>

**Which of the following code snippets will count the number of occurrences of a substring in a string in Python?**

a) string.count(substring)\
b) string.occurrences(substring)\
c) string.find(substring)\
d) string.index(substring)

<details>

<summary>Solution</summary>

Answer: a) string.count(substring)

</details>

**Which of the following code snippets will check if all characters in a string are alphanumeric in Python?**

a) string.is\_alpha\_num()\
b) string.is\_alphanumeric()\
c) string.isalpha() and string.isdigit()\
d) string.isalnum()

<details>

<summary>Solution</summary>

Answer: d) string.isalnum()

</details>

**Which of the following code snippets will convert a string to a list of words in Python?**

a) string.split()\
b) string.words()\
c) list(string)\
d) string.list\_words()

<details>

<summary>Solution</summary>

Answer: a) string.split()

</details>

**Which of the following code snippets will check if a string ends with a specific substring in Python?**\\

a) string.end(substring)\
b) string.check\_end(substring)\
c) string.endswith(substring)\
d) string.ends(substring)

<details>

<summary>Solution</summary>

Answer: c) string.endswith(substring)

</details>

**Which of the following code snippets will return the index of the first occurrence of a substring in a string in Python?**

a) string.find(substring)\
b) string.index(substring)\
c) string.first(substring)\
d) string.search(substring)\
e) Both **a** and **b**

<details>

<summary>Solution</summary>

Answer: option **e**

</details>

**Which of the following code snippets will check if all characters in a string are in lowercase in Python?**

a) string.islower()\
b) string.is\_lowercase()\
c) string.islowercase()\
d) string.is\_lower\_case()

<details>

<summary>Solution</summary>

Answer: a) string.islower()

</details>

**Which of the following code snippets will remove all occurrences of a character in a string in Python?**

a) string.remove(char)\
b) string.delete(char)\
c) string.replace(char, '')\
d) string.sub(char, '')

<details>

<summary>Solution</summary>

Answer: c) string.replace(char, '')

</details>

**Which of the following code snippets will check if all characters in a string are in uppercase in Python?**

a) string.is\_uppercase()\
b) string.isupper()\
c) string.is\_upper()\
d) string.is\_upper\_case()

<details>

<summary>Solution</summary>

Answer: b) string.isupper()

</details>
