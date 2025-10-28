# Hamming distance

Example: The hamming distance between RAT and SAT will be 1. As only 1 character from both strings (R and S) is different.\\

```
def hamming_distance(str1, str2):
    if len(str1) != len(str2):
        print("Error: Input strings must have the same length")
        return None
    else:
        distance = 0
        for char1, char2 in zip(str1, str2):
            if char1 != char2:
                distance += 1

        return distance


string1 = input("Enter the first string: ")
string2 = input("Enter the second string: ")

distance = hamming_distance(string1, string2)

if distance is not None:
    print(f"The Hamming distance between '{string1}' and '{string2}' is: {distance}")

```
