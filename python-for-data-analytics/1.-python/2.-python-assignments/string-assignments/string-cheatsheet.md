# String CheatSheet

## String CheatSheet

1. **Concatenation(+)** : It joins a string with another string.\
   \
   `str1='hi I am'`\
   `str2='ayush'`\
   `result= str1 + str2 # str3='hi I am ayush'`
2. **Repitition( \* )**: It repeats a string.\
   \
   `str='ayush'`\
   `result= str * 3 # ayushayushayush`
3. **Membership Operator:**
   1. **in** : It checks the presence of a substring in a string.\
      \
      `str1='hi I am Ayush'`\
      `result= 'I' in str1 # True`
   2. **not in:** It checks the absence of a subtring in a string.\
      \
      `str1='hi I am Ayush'`\
      `result='z' in str1 # True`
4. **len():** It gives the length (number of characters) of the string.\
   \
   `str1='hi i am Ayush'`\
   `result= len(str1) # 13`
5. **max()**: It gives the maximum value character in a string.\
   \
   `str1='Ayush'`\
   `result=max(str1) # y`
6. **min()**: It gives the minimum value character in a string.\
   \
   `str1='Ayush'`\
   `result=min(str1) # A`
7. **.lower()**: It converts all the characters of a string to Lower case.\
   \
   `str1='AYUSH'`\
   `result=str1.lower() # ayush`
8. **.upper()**: It converts all the characters of a string to upper case.\
   \
   `str1='ayush'`\
   `result=str1.upper() # 'AYUSH'`
9. **.capitalize():** It capitalizes the first character of the string only.\
   \
   `str1='HI I AM AYUSH'`\
   `result=str1.capitalize() # Hi i am ayush`
10. **.title():** It capitalizes the first letter of each word in the string.\
    \
    `str1='HI I AM AYUSH'`\
    `result=str1.title() # Hi I Am Ayush`
11. **.swapcase():** It converts all lowercase characters to uppercase and all uppercase characters to lowercase within the string.\
    \
    `str1=' Hi I aM aYUsh'`\
    `result= str1.swapcase() # hI i Am AyuSH`
12. **.strip():** It removes all whitespaces from left and right side of the string.\
    \
    `str1=' ayush '`\
    `result=str1.strip() # ayush`
13. **.lstrip():** It removes all whitespaces from left side of the string only.\
    \
    `str1=' ayush '`\
    `result= str1.lstrip() # ayush (includes spaces present on the right side)`
14. **.rstrip():**&#x49;t removes all whitespaces from right side of the string only.\
    \
    `str1=' ayush '`\
    `result=str1.rstrip() # ayush (includes spaces on the left side)`
15. **.replace(old,new):** Replaces all occurrences of the "old" substring with the "new" substring.\
    \
    `str1='python is python and python is good.'`\
    `result=str1.replace('Python','java') # java is java and java is good.`\
    \
    \&#xNAN;**.replace(old,new,count):** Replaces old substring with the new substring depending upon the counting provide.\
    \
    `str1='python is python and python is good'`\
    `result=str1.replace('python','java',2) # java is java and python is good.`
16. **.count('substring'):** It gives the counting of a substring in the string.\
    \
    `str1='python is python and python is good'`\
    `result=str1.count('o') # 5`\
    \
    \&#xNAN;**.count('substring',start,end):** It gives the counting of a substring in the string. Counting starts from **start** index no. and **ends at end** index number.\
    \
    `str1='python is python and python is good'`\
    `result=str1.count('o',15,35) # 3`
17. **.find('substring'):** It gives the index number of the first appearance of the substring.\
    \
    `str1='python is python and python is good'`\
    `result=str1.find('y') # 1`\
    \
    \&#xNAN;**.find('substring',start,end):** It gives the index number of the first appearance of the substring starting from start point.\
    \
    `str1='python is python'`\
    `result=str1.find('y',2,15) # 11`
18. **.rfind('substring'):** It gives the index number of the first appearance of the substring from the right side.\
    \
    `str1='python is python'`\
    `result=str1.rfind('y') # 11`
19. **.index('substring'):** It gives the index number of the first appearance of the substring.\
    \
    `str1='python is python and python is good'`\
    `result=str1.find('y') # 1`\
    \
    \&#xNAN;**.index('substring',start,end):** It gives the index number of the first appearance of the substring starting from start point.\
    \
    `str1='python is python'`\
    `result=str1.find('y',2,15) # 11`
20. **.rindex('substring'):** It gives the index number of the first appearance of the substring from the right side.\
    \
    `str1='python is python'`\
    `result=str1.rfind('y') # 11`
21. **.split(separator):** It breaks a string into multiple substrings depending upon the separator. Default separater is 'space'.\
    \
    `str1='python is a programming language'`\
    `result=str1.split() #['python','is','a','programming','language']`\
    \
    **split(separator,maxsplit):** It breaks a string into multiple substrings depending upon the separator. Default separater is 'space'.Maxsplit defines the number of breaks you want of a string.\
    \
    `str1='python is a programming language'`\
    `result=str1.split(' ',2) #['python','is','a programming language']`
22. **.rsplit(separator):** It breaks a string into multiple substrings depending upon the separator. Default separater is 'space'.\
    \
    `str1='python is a programming language'`\
    `result=str1.rsplit() #['python','is','a','programming','language']`\
    \
    **rsplit(separator,maxsplit):** It breaks a string into multiple substrings depending upon the separator. Default separater is 'space'.Maxsplit defines the number of breaks you want of a string.\
    \
    `str1='python is a programming language'`\
    `result=str1.rsplit(' ',2) #['python is a','programming', 'language']`
23. **.partition():** It breaks a string depending upon the separater but only once and also includes the separator in the output.\
    \
    `str1='python is a programming language'`\
    `result=str1.partition(' ') # ('python',' ' ,'is a programming language')`\
    \
    \&#xNAN;**.rpartition():** It breaks a string depending upon the separater but only once and also includes the separator in the output.\
    \
    `str1='python is a programming language'`\
    `result=str1.rpartition(' ') # ('python is a programming',' ', 'language')`
24. **.islower():** It checks whether all the alphabets in a string are in lower case or not.\
    \
    `str1='ayush'`\
    `result=str1.islower() # True`
25. **.isupper():** It checks whether all the alphabets in a string are in upper case or not.\
    \
    `str1='AYUSH'`\
    `result=str1.isiupper() # True`
26. **.alpha():** It checks whether all the characters in a string are alphabet or not.\
    \
    `str1='ayush'`\
    `result=str1.alpha() # True`
27. **.isnumeric():** It checks whether all the characters in a string are digit or not.\
    \
    `str1='12345'`\
    `result=str1.isnumeric() # True`
28. **.isalnum():** It checks whether all the characters in a string are alphabet or digits only.\
    \
    `str1='ayush12345'`\
    `result=str1.isalnum # True`
29. **.startswith():** It checks whether the string starts with a particular substring or not.\
    \
    `str1='+91 1234567890'`\
    `result=str1.startswith('+91') # True`
30. **.endswith():** It checks whether the string ends with a particular substring or not.\
    \
    `str1='myfile.txt'`\
    `result=str1.endswith('txt') # True`
