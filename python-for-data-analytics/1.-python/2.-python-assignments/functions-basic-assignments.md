# Functions- Basic Assignments

1. Create a non-return type function that takes the user's name and display the message\
   "Hello user! Welcome to Python Functions"

<details>

<summary>Solution</summary>

```python
def greeting(user_name):
    print('Hello',user_name,'!Welcome to Python Functions')
    
name=input('Enter your name:')
greeting(name)
```

</details>

2. Create a non-return type function that takes the details of user like name,age, city, company, and profile and display the message-\
   "Hello Python, I am name. I am age years old. I am a profile in company"

<details>

<summary>Solution</summary>

```python
def introduction(user_name,user_age,user_profile,user_company):
    print('Hello Python, I am',user_name,'.I am',user_age,'years old. I am a',user_profile,'in',user_company,'.')

name=input('Enter your name:')
age=int(input('Enter your age:'))
profile=input('Enter Your profile:')
company=input('Enter your company:')

introduction(name,age,profile,company)

```

</details>

3. Create a return type function that takes the length and breadth of a rectangle and calculate area of the rectangle.

<details>

<summary>Solution</summary>

```python
def area_of_rectangle(length,breadth):
    area=length * breadth
    return area

length=int(input('Length of the rectangle:'))
breadth=int(input('breadth of the rectangle:'))

print('Area of the rectangle is ',area_of_rectangle(length,breadth))
```

</details>

4. Create a return type function that takes weight and height of a user and return the bmi of the user.\
   Depending upon the bmi show the category that the custimer belongs to.

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2F9pQ2QH9oIUxU3kt2Yl90%2Fimage.png?alt=media&#x26;token=bb89e37e-e495-4761-a90d-4dd33558c61d" alt=""><figcaption></figcaption></figure>

<details>

<summary>Solution</summary>

```python
def calculate_BMI(weight,height):
    bmi=round(weight / height ** 2 * 10000)
    return bmi


w=int(input('enter Weight:'))
h=int(input('enter height:'))
bmi=calculate_BMI(w,h)
print('Your BMI is:',bmi)

print('Your Category:')

print('Underweight:',bmi<18.5)
print('Normal range:',bmi>=18.5 and bmi<=24.9)
print('Overweight:',bmi>=25.0 and bmi<=29.9)
print('Obese:',bmi>=30)
```

</details>

5. Create a return type function that takes principle, rate, and time from the user and then return simple interest after calculation.Afterwards Calculate amount that the user has to repay.

<details>

<summary>Solution</summary>

```python
def calculate_simple_interest(principle,rate,time):
    simple_interest=principle * rate * time / 100
    return simple_interest

principle=int(input('Enter principle:'))
rate=int(input('Enter Rate:'))
time=int(input('Enter time:'))

si=calculate_simple_interest(principle,rate,time)
print('Your interest charged will be:',si)

amount=principle + si
print('Amount you will repay is',amount,'Rs')

```

</details>

6. Create a return function that takes the radius and height of a cylinder and return the total surface area.\
   TSA = 2πr\*(r + h).

<details>

<summary>Solution</summary>

```python
def total_surface_area_cylinder(radius,height,pi=3.14):
    total_surface_area = 2 * pi * radius *(radius + height)
    return total_surface_area

radius= int(input('Enter radius of the cylinder:'))
height= int(input('Enter height of the cylinder:'))

print('the total surface area of the cylinder is',total_surface_area_cylinder(radius,height))
```

</details>

7. Create a function that takes the radius and height of a cone and return the volume.\
   V=1/3hπr²

<details>

<summary>Solution</summary>

```python
def volume_of_cone(radius,height,pi=3.14):
    volume = (pi * radius ** 2 * height) * 1 / 3
    return volume


radius= int(input('Enter radius of the cone:'))
height= int(input('Enter height of the cone:'))


v= volume_of_cone(radius,height)
print('Volumeof the cone',v)
```

</details>

8. Create a function that returns the quotient and remainder after dividing two numbers.

<details>

<summary>Solution</summary>

```python
def calculate_quotient_remainder(num1,num2):
    res1=num1//num2
    res2=num1%num2
    return res1,res2

a=int(input('enter first number:'))
b=int(input('enter second number:'))

quot,rem=calculate_quotient_remainder(a,b)

print('quotient:',quot)
print('remainder:',rem)

```

</details>

9. Create a return type function that takes marks of 5 subjects from a student and calculates the percentage of the student.

<details>

<summary>Solution</summary>

```python
def percentage(m1,m2,m3,m4,m5):
    sum=m1+m2+m3+m4+m5
    percent= sum * 100/500
    return percent

phys=int(input('Enter Physics marks:'))
chem=int(input('Enter chemistry marks:'))
maths=int(input('Enter maths marks:'))
hindi=int(input('Enter hindi marks:'))
english=int(input('Enter english marks:'))

per=percentage(phys,chem,maths,hindi,english)

print('Your percentage is:',per,'%')
```

</details>

10. Create a function called create\_bill that takes product name,price, and qty and return the bill.

<details>

<summary>Solution</summary>

```python
def create_bill(product_name,product_price,product_qty):
    bill=product_price * product_qty
    return bill

product=input('enter name of the product:')
price=int(input('enter price:'))
quantity=int(input('Enter quantity:'))

amount=create_bill(product,price,quantity)

print('The bill of',product,'of',price,'Rs for',quantity,'pieces is Rs',amount)
```

</details>
