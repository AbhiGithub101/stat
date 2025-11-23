# Dictionary Cheatsheet

## Dictionary Cheatsheet

ex: `my_dict = {'name': 'John', 'age': 25, 'city': 'New York'}`

1. **.clear():** Removes all items from the dictionary.\
   \
   `my_dict.clear() # {}`\\
2. **.copy():** Creates a copy of a dictionary\
   \
   `new_dict=my_dict.copy() #{'name':'John', 'age':25, 'city':'New York'}`\\
3. **.get():** Returns the value of a particular key.\
   \
   `my_dict.get('age') # 25`\\
4. **.items():** Returns all the items preent int he dictionary as (key,value) pairs.\
   \
   `my_dict.items() # (name,john), (age,25),(city,New York)`\\
5. **.keys():** Returns a list of keys in a dictionary\
   \
   `my_dict.keys() # [name,age,city]`\\
6. **.values():** Returns a list of values in a dictionary.\
   \
   `my_dict.values() # [john,25,new york]`\\
7. **.pop(key):** Removes the key value pair from the dictionary.\
   \
   `my_dict.pop('age') # {'name': 'John', 'city': 'New York'}`\\
8. **.popitem():** Removes the last key value pair from the dictionary.\
   \
   `my_dict.popitem() # {'name': 'John', 'age': 25}`<br>
9. **.upate():** Updates a dictionary by adding the items from another dictionary.\
   \
   `new_dict={'country':'USA','mob_num':12345}`\
   `my_dict.update(new_dict)`\
   \
   `# {'name': 'John', 'age': 25, 'city': ' New York','country':'USA','mob_num':12345}`\\
10. **.setdefault(key,value):**&#x52;eturns the value for a key if it exists. If not, inserts the key with a value of default and returns default.\
    \
    `my_dict.setdefault('age', 30) # {'name': 'John', 'age': 25, 'city': 'New York'}`\
    `my_dict.setdefault('height', 175) # {'name': 'John', 'age': 25, 'city': 'New York','height',175}`\\
11. **.fromkeys():**&#x43;reates a new dictionary with keys from iterable and values set to value.\
    \
    `new_dict =dict.fromkeys(['a', 'b', 'c'], 0) # {'a': 0, 'b': 0, 'c': 0}`
