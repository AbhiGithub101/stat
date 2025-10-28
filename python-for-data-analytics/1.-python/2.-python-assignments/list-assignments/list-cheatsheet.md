# List Cheatsheet

## List Cheatsheet

1. .**append(item):** To add an item in a list.\
   \
   `l1=[12,23,34,56]`\
   `l1.append(3.14) # [12,23,34,56,3.14]`\\
2. **.extend(list):** To add a list in a list\
   \
   `l1=[12,23,34,56]`\
   `l2=['a','b','c'] # [12,23,34,56,'a','b','c']`\\
3. **.insert(index,item):** To add an item at a particular index in a list\
   \
   `l1=[12,23,34,56]`\
   `l1.insert(2,420) # [12,23,420,34,56]`\\
4. **.remove(item):** To remove an item from the list\
   \
   `l1=[12,23,34,56]`\
   `l1.remove(34) # [12,23,56]`\\
5. .**pop(index):** To remove an item fromt the list on behalf of index number\
   \
   `l1=[12,23,34,56]`\
   `l1.pop(1) # [12,34,56]`\\
6. **.index(item):** It provides the index number of an item.\
   \
   `l1=[12,23,34,56]`\
   `l1.index(23) # 1`\\
7. **.count(item)**: It provide the counting of an item in a list\
   \
   `l1=[12,23,34,56,34,34]`\
   `l1.count(34) # 3`\\
8. **.sort():** It arranges the items of a list in an ascending order\
   \
   `l1=[90,121,1,2,23,34,5,6]`\
   `l1.sort() # [1,2,5,6,23,34,90,121]`\\
9. .**reverse()**: It reverse the items from first to last in a list\
   \
   `l1=[90,121,1,2,23,34,5,6]`\
   `l1.reverse() # [6,5,34,23,2,1,121,90]`\\
10. **.copy():** It copies item of one list to another list\
    \
    `l1=[90,121,1,2,23,34,5,6]`\
    `l2=l1.copy() # [90,121,1,2,23,34,5,6]`\\
11. **.clear():** It removes all the items of a list in one go.\
    \
    `l1=[90,121,1,2,23,34,5,6]`\
    `l1.clear() # []`
