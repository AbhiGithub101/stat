# Sets Cheatsheet

## Sets Cheatsheet

1. **.add(item):** Adds a single item in a set\
   \
   `s1={12,34,23,56,78,45}`\
   `s1.add(3.14) # {12,34,23,56,78,45,3.14}`\\
2. **.upate(iterables):** Updates a set by adding an iterable(list,set,tuple) in a set.\
   \
   `s1={12,34,23,56,78,45}`\
   `s1.update([1.23,4.20,5.67]) # {12,1.23,23,34,4.20,45,56,78,5.67}`\\
3. **.union(set):** Returns a snew set consist of items from both sets.\
   \
   `s1={12,34,23,56,78,45}`\
   `s2={1.23,4.20,5.67}`\
   `s1.union(s2) # {12,1.23,23,34,4.20,45,56,78,5.67}`\\
4. **.remove(item):** Removes a specific item from the set.\
   \
   `s1={12,34,23,56,78,45}`\
   `s1.remove(56) # {12,34,23,78,45}`\\
5. **.discard(item):** Removes a specific item from the set.\
   \
   `s1={12,34,23,56,78,45}`\
   `s1.discard(34) # {12,23,56,78,45}`\\
6. **.pop():** Removes an item randomly from the set.\
   \
   `s1={12,34,23,56,78,45}`\
   `s1.pop() # {12,34,23,56,45}`\\
7. **.clear():** Removes all the items from the set.\
   \
   `s1={12,34,23,56,78,45}`\
   `s1.clear() # set()`\\
8. **.copy(set):** Copies items of one set into another\
   \
   `s1={12,34,23,56,78,45}`\
   `s2=s1.copy() # s2={12,34,23,56,78,45}`\\
9. **.intersection(set):** Returns a new set with common items from both the sets\
   \
   `s1={12,34,23,56,78,45}`\
   `s2={1,2,34,56,78,9,11}`\
   `s1.intersection(s2) # {34,56,78}`\\
10. **.difference():** Returns a new set with the items in the first set but not in the second.\
    \
    `s1={12,34,23,56,78,45}`\
    `s2={1,2,34,56,78,9,11}`\
    `s1.difference(s2) # {12,23,45}`\\
11. **.symmetric\_difference():** Returns a new set with uncommon items from both sets.\
    \
    `s1={12,34,23,56,78,45}`\
    `s2={1,2,34,56,78,9,11}`\
    `s1.symmetric_difference(s2) # {12,23,45,1,2,9,11}`
