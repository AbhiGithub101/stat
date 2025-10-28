# Introduction To BeautifulSoup

#### Problem Statement:

In our previous session, we have already built a normal webpage. If we try to scrape the data from our e-commerce website, with python only, it is going to be complicated. So we need **BeautifulSoup Library** to extract data from HTML Document.

Beautiful Soup is a Python library for getting data out of **HTML, XML,** and other markup languages. Say you’ve found some webpages that display data relevant to your research, such as date or address information, but that do not provide any way of downloading the data directly. Beautiful Soup helps you pull particular content from a webpage, remove the HTML markup, and save the information. It is a tool for **web scraping** that helps you clean up and parse the documents you have pulled down from the web.

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FvJXPc0WiDdndVc6BcZDq%2Fimage.png?alt=media&#x26;token=d38b882f-95c9-4899-af3b-874665cd7b15" alt=""><figcaption></figcaption></figure>

So let's try to scrape the HTML Document that we have created in previous Document.

#### Import BeautifulSoup:

```python
from bs4 import BeautifulSoup
```

#### Store HTML Document in a variable:

```python
from bs4 import BeautifulSoup

html_doc = '''<html>
  <head>
    <title>
      E-Commerce Website
    </title>

  </head>

<div class="Phone">
    <h1>Samsung Galaxy</h1>
    <img src="https://rukminim1.flixcart.com/image/312/312/l4n2oi80/mobile/x/o/a/-original-imagfhu75eupxyft.jpeg?q=70">
    <ol>
      <li>16.76 cm (6.6 inch) Full HD+ Display</li>
      <li>50MP + 5MP + 2MP | 8MP Front Camera</li>
      <li>6000 mAh Lithium Ion Battery</li>
    </ol>
    <a href="https://www.flipkart.com/samsung-galaxy-f13-waterfall-blue-64-gb/p/itm583ef432b2b0c?pid=MOBGENJWBPFYJSFT&lid=LSTMOBGENJWBPFYJSFT1ZY7B0&marketplace=FLIPKART&q=phone&store=tyy%2F4io&srno=s_1_1&otracker=search&otracker1=search&fm=organic&iid=295e999b-0776-4804-a75d-0a85601f9997.MOBGENJWBPFYJSFT.SEARCH&ppt=hp&ppn=homepage&ssid=toxfkh39a80000001664350650062&qH=f7a42fe7211f98ac">
      Know More
    </a>
  </div>

<div class="Phone">
    <h1>Redmi</h1>
    <img src="https://rukminim1.flixcart.com/image/312/312/l0tweq80/mobile/x/f/u/-original-imagcgtghym8theg.jpeg?q=70">
    <ol>
      <li>16.76 cm (6.6 inch) Full HD+ Display</li>
      <li>50MP + 5MP + 2MP | 8MP Front Camera</li>
      <li>6000 mAh Lithium Ion Battery</li>
    </ol>
    <a href="https://www.flipkart.com/samsung-galaxy-f13-waterfall-blue-64-gb/p/itm583ef432b2b0c?pid=MOBGENJWBPFYJSFT&lid=LSTMOBGENJWBPFYJSFT1ZY7B0&marketplace=FLIPKART&q=phone&store=tyy%2F4io&srno=s_1_1&otracker=search&otracker1=search&fm=organic&iid=295e999b-0776-4804-a75d-0a85601f9997.MOBGENJWBPFYJSFT.SEARCH&ppt=hp&ppn=homepage&ssid=toxfkh39a80000001664350650062&qH=f7a42fe7211f98ac">
      Know More
    </a>
  </div>

<div class="Phone">
    <h1>Real Me</h1>
    <img src="https://rukminim1.flixcart.com/image/312/312/xif0q/mobile/w/o/s/-original-imaghuf9mryjhf3m.jpeg?q=70">
    <ol>
      <li>3 GB RAM | 32 GB ROM | Expandable Upto 1 TB</li>
      <li>16.51 cm (6.5 inch) HD+ Display</li>
      <li>50MP + 0.3MP | 5MP Front Camera</li>
    </ol>
    <a href="https://www.flipkart.com/realme-c33-sandy-gold-32-gb/p/itma112335dbe78a?pid=MOBGHBJGF9QZYSZX&lid=LSTMOBGHBJGF9QZYSZXROLVZH&marketplace=FLIPKART&q=phone&store=tyy%2F4io&srno=s_1_3&otracker=search&otracker1=search&fm=organic&iid=7afc7ac2-3c21-4e15-90ca-cd8927f30950.MOBGHBJGF9QZYSZX.SEARCH&ppt=hp&ppn=homepage&ssid=p1v9d2ol9s0000001664366204064&qH=f7a42fe7211f98ac">
      Know More
    </a>
  </div>

<div class="Laptop">
    <h1>Asus</h1>
    <img src="https://rukminim1.flixcart.com/image/312/312/kp2y2kw0/computer/y/0/c/na-thin-and-light-laptop-asus-original-imag3ebnzawky4kn.jpeg?q=70">
    <ol>
      <li>Intel Core i3 Processor (10th Gen)</li>
      <li>8 GB DDR4 RAM</li>
      <li>64 bit Windows 11 Operating System</li>
    </ol>
    <a href="https://www.flipkart.com/asus-vivobook-15-2022-core-i3-10th-gen-8-gb-512-gb-ssd-windows-11-home-x515ja-ej362ws-x515ja-ej392ws-thin-light-laptop/p/itmae4a34193296d?pid=COMG87FFPEDAAGXW&lid=LSTCOMG87FFPEDAAGXWTMCIPI&marketplace=FLIPKART&q=Laptop&store=6bo%2Fb5g&spotlightTagId=BestsellerId_6bo%2Fb5g&srno=s_1_1&otracker=search&otracker1=search&fm=Search&iid=ca1d4d5b-2450-482a-9e57-e9df17fd1a29.COMG87FFPEDAAGXW.SEARCH&ppt=sp&ppn=sp&ssid=29es49sv8g0000001664367547326&qH=146bdebb324a64d3">
      Know More
    </a>
  </div>

<div class="Laptop">
    <h1>HP</h1>
    <img src="https://rukminim1.flixcart.com/image/312/312/kbqu4cw0/computer/q/x/r/hp-original-imaftyzachgrav8f.jpeg?q=70">
    <ol>
      <li>AMD Ryzen 5 Hexa Core Processor</li>
      <li>8 GB DDR4 RAM</li>
      <li>64 bit Windows 11 Operating System</li>
    </ol>
    <a href="https://www.flipkart.com/hp-pavilion-ryzen-5-hexa-core-amd-r5-5600h-8-gb-512-gb-ssd-windows-10-4-graphics-nvidia-geforce-gtx-1650-144-hz-15-ec2004ax-gaming-laptop/p/itm98c94bbf9bc20?pid=COMG5GZXPWMGTNWS&lid=LSTCOMG5GZXPWMGTNWSQE9WVW&marketplace=FLIPKART&q=Laptop&store=6bo%2Fb5g&srno=s_1_4&otracker=search&otracker1=search&fm=Search&iid=ca1d4d5b-2450-482a-9e57-e9df17fd1a29.COMG5GZXPWMGTNWS.SEARCH&ppt=sp&ppn=sp&ssid=29es49sv8g0000001664367547326&qH=146bdebb324a64d3">
      Know More
    </a>
  </div>

</html>'''

```

#### Convert HTML Document in a BeautifulSoup Object:

You need to convert your HTML Document in a BeautifulSoup Object, if you want to scrape data from HTML Doc efficiently. We will also need a parser **`"lxml"`** that converts Document in a meaningful structure so that scraping can be done easily.

```python
soup = BeautifulSoup(html_doc,'lxml')
```

#### To read HTML Document:

```python
print(soup.prettify())
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FpxLw1jgDkr5QGbBgSZlm%2Fimage.png?alt=media&#x26;token=eef17d0f-df14-40cf-8551-8a183ec8ad1c" alt=""><figcaption></figcaption></figure>

#### To Navigate through Structure :

**To get `<title>` tag from html document :**

```python
soup.title

Output : <title>
      E-Commerce Website
    </title>
```

If you only want text inside `<title>` tag. We can use `get_text()` method. It returns a string value.

```python
soup.title.get_text()

Output : E-Commerce Website
```

**find() method -> To get first div tag with class "Phone" :**

{% hint style="info" %}
**find() method gives you the first occurence of the tag that you want to find.**
{% endhint %}

If you want to find something specific, we may need to use attributes. Like if you watch HTML Code carefully, First div tag has an attribute **`'class = 'Phone'.`**

We will use find() method to get our desired result.

```python
phone = soup.find('div',attrs={'class':{'Phone'}})
print(phone)

Output (First instance of Phone) : 

<div class="Phone">
<h1>Samsung Galaxy</h1>
<img src="https://rukminim1.flixcart.com/image/312/312/l4n2oi80/mobile/x/o/a/-original-imagfhu75eupxyft.jpeg?q=70"/>
<ol>
<li>16.76 cm (6.6 inch) Full HD+ Display</li>
<li>50MP + 5MP + 2MP | 8MP Front Camera</li>
<li>6000 mAh Lithium Ion Battery</li>
</ol>
<a href="https://www.flipkart.com/samsung-galaxy-f13-waterfall-blue-64-gb/p/itm583ef432b2b0c?pid=MOBGENJWBPFYJSFT&amp;lid=LSTMOBGENJWBPFYJSFT1ZY7B0&amp;marketplace=FLIPKART&amp;q=phone&amp;store=tyy%2F4io&amp;srno=s_1_1&amp;otracker=search&amp;otracker1=search&amp;fm=organic&amp;iid=295e999b-0776-4804-a75d-0a85601f9997.MOBGENJWBPFYJSFT.SEARCH&amp;ppt=hp&amp;ppn=homepage&amp;ssid=toxfkh39a80000001664350650062&amp;qH=f7a42fe7211f98ac">
      Know More
    </a>
</div>
```

So we got details about our first phone inside `<div>` tag.

**contents -> To get contents of any tag:**

contents returns a list of all the child tags inside Parent tag that is `<div>` here.

```python
phone.contents

[<h1>Samsung Galaxy</h1>, 
<img src="https://rukminim1.flixcart.com/image/312/312/l4n2oi80/mobile/x/o/a/-original-imagfhu75eupxyft.jpeg?q=70"/>, 
<ol> <li>16.76 cm (6.6 inch) Full HD+ Display</li> <li>50MP + 5MP + 2MP | 8MP Front Camera</li> <li>6000 mAh Lithium Ion Battery</li></ol>, 
<a href="https://www.flipkart.com/samsung-galaxy-f13-waterfall-blue-64-gb/p/itm583ef432b2b0c?pid=MOBGENJWBPFYJSFT&amp;lid=LSTMOBGENJWBPFYJSFT1ZY7B0&amp;marketplace=FLIPKART&amp;q=phone&amp;store=tyy%2F4io&amp;srno=s_1_1&amp;otracker=search&amp;otracker1=search&amp;fm=organic&amp;iid=295e999b-0776-4804-a75d-0a85601f9997.MOBGENJWBPFYJSFT.SEARCH&amp;ppt=hp&amp;ppn=homepage&amp;ssid=toxfkh39a80000001664350650062&amp;qH=f7a42fe7211f98ac">  
Know More</a>]

```

To better understand, contents return a list of different tags so we can find it by indexing.

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FX3m9fOjQf80iuRkarbL3%2Fimage.png?alt=media&#x26;token=2fc457d8-6daf-4146-9e6c-e98d635576bb" alt=""><figcaption></figcaption></figure>

```python
name = phone.contents[0].get_text()
specifications = phone.contents[2].get_text()
print(name)
print(specifications)

Output : 

Samsung Galaxy
 16.76 cm (6.6 inch) Full HD+ Display 50MP + 5MP + 2MP | 8MP Front Camera 6000 mAh Lithium Ion Battery

```

**To get name of the phone using find() method :**

As you can see , name of the phone is in `<h1>` tag, So we can find it by **find()** method.

```python
name = phone.find('h1').get_text()
print('Name : ', name)

Output : 
Name :  Samsung Galaxy
```

**To get Link of the image :**

If you see first div tag , `<img>` tag has the link in `src` attribute. We can use this attribute to get the link of the image. You can get it simply by doing this:

```python

image = phone.find('img')['src']
print(image)

Output:

https://rukminim1.flixcart.com/image/312/312/l4n2oi80/mobile/x/o/a/-original-imagfhu75eupxyft.jpeg?q=70
```

**find\_all() ---> To get all the specifications of our phone :**

`find()` method only gives the first occurence of any particular tag, but `find_all()` method gives all occurences that returns a list of tags.

let us say we use find method for `<li>` to get specification.

**using find() method to get specification.**

```python
spec = phone.find('li')
print(spec)
print(spec.get_text())

Output : 

<li>16.76 cm (6.6 inch) Full HD+ Display</li>
16.76 cm (6.6 inch) Full HD+ Display  
```

> As you can see there are multiple specifications, but we got the first instance only.

**using find\_all() method to get all specifications.**

```python

specs = phone.find_all('li')
print(specs)

Output : 

[<li>16.76 cm (6.6 inch) Full HD+ Display</li>, 
<li>50MP + 5MP + 2MP | 8MP Front Camera</li>,
 <li>6000 mAh Lithium Ion Battery</li>]
```

**Using loop to get all the texts from the lists.**

```python
specs = phone.find_all('li')

for spec in specs:
    print(spec.get_text())


Output:
16.76 cm (6.6 inch) Full HD+ Display
50MP + 5MP + 2MP | 8MP Front Camera
6000 mAh Lithium Ion Battery
```

**get link to know more about phone :**

To get link , we need to get `<a>` tag and its `<href>` attribute.

```python
link = phone.find('a')['href']
print(link)


Output:
https://www.flipkart.com/samsung-galaxy-f13-waterfall-blue-64-gb/p/itm583ef432b2b0c?pid=MOBGENJWBPFYJSFT&lid=LSTMOBGENJWBPFYJSFT1ZY7B0&marketplace=FLIPKART&q=phone&store=tyy%2F4io&srno=s_1_1&otracker=search&otracker1=search&fm=organic&iid=295e999b-0776-4804-a75d-0a85601f9997.MOBGENJWBPFYJSFT.SEARCH&ppt=hp&ppn=homepage&ssid=toxfkh39a80000001664350650062&qH=f7a42fe7211f98ac
```

#### Assignment 1 : Try to combine everything and get info about our Phone.

**Output should be Something** **like this:**

```
Name :  Samsung Galaxy

Picture :  https://rukminim1.flixcart.com/image/312/312/l4n2oi80/mobile/x/o/a/-original-imagfhu75eupxyft.jpeg?q=70

Specifications : 
> 16.76 cm (6.6 inch) Full HD+ Display
> 50MP + 5MP + 2MP | 8MP Front Camera
> 6000 mAh Lithium Ion Battery

Know More :  https://www.flipkart.com/samsung-galaxy-f13-waterfall-blue-64-gb/p/itm583ef432b2b0c?pid=MOBGENJWBPFYJSFT&lid=LSTMOBGENJWBPFYJSFT1ZY7B0&marketplace=FLIPKART&q=phone&store=tyy%2F4io&srno=s_1_1&otracker=search&otracker1=search&fm=organic&iid=295e999b-0776-4804-a75d-0a85601f9997.MOBGENJWBPFYJSFT.SEARCH&ppt=hp&ppn=homepage&ssid=toxfkh39a80000001664350650062&qH=f7a42fe7211f98ac

```

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

```python
from bs4 import BeautifulSoup

html_doc = '''<html>....</html>'''

html_doc=html_doc.replace('\n','')
soup = BeautifulSoup(html_doc,'lxml')

phone = soup.find('div',attrs={'class':{'Phone'}})

name = phone.find('h1').get_text()
print('Name : ',name)
pic = phone.find('img')['src']
print('Picture : ',pic)
specs = phone.find_all('li')
print('Specifications : ')
for spec in specs:
    print('>',spec.get_text())
link = phone.find('a')['href']
print('Know More : ',link)

```

</details>

#### Try to get details of all phones:

Now that we have got details of a single phone , we can use `find_all()` method to find all the phones and then scrape data of phones by using loop.

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

```python
phones = soup.find_all('div',attrs={'class':{'Phone'}})

for phone in phones:
    name = phone.find('h1').get_text()
    print(f'-----------------------------{name}------------------------------')
    print('Name : ',name)
    pic = phone.find('img')['src']
    print('Picture : ',pic)
    specs = phone.find_all('li')
    print('Specifications : ')
    for spec in specs:
        print('>',spec.get_text())
    link = phone.find('a')['href']
    print('Know More : ',link)

```

</details>

#### Assignment 2 : Try to Scrape All Laptop Details:

<details>

<summary><mark style="color:purple;">Solution</mark></summary>

```
phones = soup.find_all('div',attrs={'class':{'Laptop'}})

for phone in phones:
    name = phone.find('h1').get_text()
    print(f'-----------------------------{name}------------------------------')
    print('Name : ',name)
    pic = phone.find('img')['src']
    print('Picture : ',pic)
    specs = phone.find_all('li')
    print('Specifications : ')
    for spec in specs:
        print('>',spec.get_text())
    link = phone.find('a')['href']
    print('Know More : ',link)

```

</details>
