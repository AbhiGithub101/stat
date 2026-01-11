# User Input & Type Casting

1. **Take the name from the user and greet him in this form - Hello, username**

<details>

<summary>Solution</summary>

```python
name = input('Enter Your Name : ')
print('Hello,', name)
```

</details>

2. **`Take input of the length and breadth of a rectangle from the user and print the area of it.`**

<details>

<summary>Solution</summary>

<mark style="color:green;">`length = float(input('Enter the length : '))`</mark>

<mark style="color:green;">`breadth = float(input('Enter the breadth : '))`</mark>

<mark style="color:green;">`area = length * breadth`</mark>

<mark style="color:green;">`print('Area :', area)`</mark>

</details>

3. **`Body mass index (BMI) is a measure of body fat based on height and weight that applies to adult men and women. The Table below shows how healthy you are with respect to your BMI.`**

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2Fo15zW2f2DUcXKQzxoSze%2FBMI%20Image.webp?alt=media&#x26;token=131ef6a0-3816-4220-9941-c8f7b6b14b9f" alt=""><figcaption></figcaption></figure>

**`The Formula That we use For BMI is :`**

$$
bmi = weight(kgs)/height(cms)^2*10000
$$

**`Take Weight and height from the user and Calculate BMI.​`**

<details>

<summary>Solution</summary>

**First we will take weight and height from user with the help of user input.**

<mark style="color:green;">`weight = int(input('Enter your weight : '))`</mark>

<mark style="color:green;">`height = int(input('Enter your height : '))`</mark>

**Then we will calculate BMI , Now say if we want only two decimal values , we can use `round()` Function.**

<mark style="color:green;">`bmi = round(weight / height ** 2 * 10000)`</mark>

<mark style="color:green;">`print('Your BMI is',bmi)`</mark>

</details>

_4._ **`Take Principle, Rate, and Time From User and Calculate Simple Interest.`**

**`Formula For Simple Interest is:`**

$$
Simple Interest = Principle * Rate * Time / 100
$$

<details>

<summary>Solution</summary>

<mark style="color:green;">`principle = int(input('Enter the amount : '))`</mark>

<mark style="color:green;">`rate = int(input('Rate : '))`</mark>

<mark style="color:green;">`time = int(input('Time : '))`</mark>

<mark style="color:green;">`simple_interest = principle * rate * time / 100`</mark>

<mark style="color:green;">`print('Simple Interest is',simple_interest)`</mark>

</details>

5\. **`Your task is to take name and age and location from user and print the following message :`**

**`Hello Everyone , I am xyz and i am xyz years old and i live in xyz.`**

<details>

<summary>Solution</summary>

<mark style="color:green;">`name = input('Enter your name : ')`</mark>

<mark style="color:green;">`age = input('What is your age ? ')`</mark>

<mark style="color:green;">`location = input('Where do you live ? ')`</mark>

<mark style="color:green;">`print('Hello Everyone , I am' ,name, 'and i am', age, 'years old and i live in', location,'.')`</mark>

</details>

**`6. Suppose there are many N numbers of people in the Army. We need to distribute them in G groups. Take the number of people from users and the Number of Groups and tell how many are left without Group.`**

<details>

<summary><em>Solution</em></summary>

<mark style="color:green;">`n = int(input('Number of Army People : '))`</mark>

<mark style="color:green;">`g = int(input('How many groups do we need ? '))`</mark>

<mark style="color:green;">`rest = n%g`</mark>

<mark style="color:green;">`print('Remaining People :',rest)`</mark>

</details>

**`7.Take Temperature in Fahrenheit and convert it into Celsius.`**

\*\*`Formula:` \*\*_**C = 5/9 \* ( F - 32 )**_

<details>

<summary>Solution</summary>

```python
# Ask user for temperature in Fahrenheit
fahrenheit = float(input("Enter temperature in Fahrenheit: "))

# Convert to Celsius
celsius = (fahrenheit - 32) * 5/9

# Print result
print(fahrenheit,' degrees Fahrenheit is equal to',celsius,'degrees Celsius.")

```

</details>

8. Take two variables from user value and power and print the solution value raised to power.\
   Such as value = 3 and power = 2 then solution is 9

<details>

<summary>Solution</summary>

```python
value = int(input('Enter the Number : '))
power = int(input('Enter the power : '))

solution = value ** power
print('Solution is', solution)
```

</details>

9. Tom had y amount in his bank and jeff withdrew x amount where x is always less than y. Print the remaining balance in Tom's account. Take x and y from the user.

<details>

<summary>Solution</summary>

```python
y = int(input("Enter Tom's account balance : "))
x = int(input('Enter withdrawal amount : '))

balance = y - x
print('Remaining balance :', balance)
```

</details>

10. Take the base and height of a triangle from the user and calculate the area of the triangle.\
    area=(base \* height)\*1/2

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FjyeJAf2mTgiWI9BdVpLv%2FRight%20angled%20triangle.png?alt=media&#x26;token=663a1a4f-5b62-4b55-8cea-6865b6fb9ded" alt=""><figcaption></figcaption></figure>

<details>

<summary>Solution</summary>

```python
base=int(input('Enter the base of the triangle:'))
height=int(input('Enter the height of the triangle:'))
area=(base*height)*1/2
print('Area of the triangle is',area)
```

</details>

11. **Take 5 numbers from the user and calculate average of those numbers.**

**(average=sum of data/number of data)**

<details>

<summary>Solution</summary>

```python
num1=int(input('Enter first number:'))
num2=int(input('Enter first number:'))
num3=int(input('Enter first number:'))
num4=int(input('Enter first number:'))
num5=int(input('Enter first number:'))

average=(num1+num2+num3+num4+num5)/5
print('Average of the numbers',average)
```

</details>

12. Take the sides of a triangle and check whether it follows Pythagoras' theorem.\
    sq. of base + sq. of height=sq. of hypotenuse

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FBQcxYboEKT0avIjEMtZ6%2FRight%20angled%20triangle.png?alt=media&#x26;token=2dd83fa6-bbd2-4e09-a110-bf427d3ede7e" alt=""><figcaption></figcaption></figure>

<details>

<summary>Solution</summary>

```python
base=int(input('Enter base of the triangle:'))
height=int(input('Enter height of the triangle:'))
hypotnuse=int(input('Enter hypotnuse of the triangle:'))
result=base**2 + height **2
print('pythagoras theorem:',result==hypotnuse**2)
```

</details>

13. Take the length and breadth of a rectangle and find the perimeter of the rectangle\
    perimeter= 2 \* (length + breadth)

<details>

<summary>Solution</summary>

```python
length=int(input('Enter length of the rectangle:'))
breadth=int(input('Enter breadth of the rectangle:'))

perimeter= 2* (length + breadth)
print('Perimeter of the rectangle with sides', length,'and',breadth,' will be', perimeter)
```

</details>

14. Take the side of a cube in cm and calculate the volume of the cube.\
    volume= side \* side \* side

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FsIqhWJCGoGd9lmZU5XH9%2FCube.png?alt=media&#x26;token=73b7b6a8-6624-4587-b8b1-444152a90542" alt=""><figcaption></figcaption></figure>

<details>

<summary>Solution</summary>

```python
side=int(input('Enter side of a cube:')
volume= side ** 3

print('Volume of the cube:',volume,'cubic cm')
```

</details>

15. Take the length, breadth, and height of a cuboid in cm and calculate the volume of the cuboid.\
    volume= length \* breadth \* height

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FuKN6kMNPperfI8B0GeBs%2FCuboid.png?alt=media&#x26;token=92f6e95c-103b-40a1-a975-9fec9c025288" alt=""><figcaption></figcaption></figure>

<details>

<summary>Solution</summary>

```python
length= int(input('Enter length of the cuboid:'))
breadth=int(input('Enter breadth of the cuboid:'))
height= int(input('Enter height of the cuboid:'))

volume= length * breadth * height
print('Volume of the cuboid:',volume,'cubic cm')
```

</details>

16. Take the radius and height of a cylinder and calculate the total surface area.\
    total\_surface\_area= 2\*3.14\* radius \*height + 2\* 3.14 \* sq. of radius

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FvFIFp5PSF24AbUSMrgRo%2FCylinder.png?alt=media&#x26;token=5558a136-3b4f-4d4e-8498-c8fae7841177" alt=""><figcaption></figcaption></figure>

<details>

<summary>Solution</summary>

```python
radius= int(input('Enter radius of the cylinder:'))
height= int(input('Enter height of the cylinder:'))
pi=3.14
total_surface_area = 2*pi*radius*height + 2*pi*radius**2
print('the total surface area of the cylinder is',total_surface_area)
```

</details>

17. Take the radius and height of a cone and calculate the volume of it.\
    volume= (3.14 \* sq of radius \* height) \* 1/3

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FFJxdGwCGX8XNrEDXRaMb%2FCone.png?alt=media&#x26;token=7c1870d9-42bd-402a-9e9c-62b21a1dc8c1" alt=""><figcaption></figcaption></figure>

<details>

<summary>Solution</summary>

```python
radius= int(input('Enter radius of the cone:'))
height= int(input('Enter height of the cone:'))
pi=3.14

volume= (pi * radius **2 *height)*1/3
print('Volumeof the cone',volume)
```

</details>

18. Take the radius and length of a cone and calculate the total surface area of it.\
    total\_surface\_area= 3.14\*radius\*(radius + length)

<details>

<summary>Solution</summary>

```python
radius= int(input('Enter radius of the cone:'))
length= int(input('Enter length of the cone:'))
pi=3.14

total_surface_area= pi * radius * (radius + length)
print('total surface area of the cone:',total_surface_area) 
```

</details>

19. The output of the following

    **A = 100**\
    **B= 30**\
    **print(A and B)**

    a. True\
    b. False\
    c. 100\
    d. 30

<details>

<summary>Solution</summary>

Answer: option **d**

</details>

20. **print(20 or 30)**

    \
    a. False\
    b. True\
    c. 20\
    d. 30

<details>

<summary>Solution</summary>

Answer: option **c**

</details>
