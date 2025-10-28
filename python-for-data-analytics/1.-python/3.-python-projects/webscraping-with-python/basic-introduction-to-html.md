# Basic Introduction To HTML

## Basic Introduction To HTML

#### Why learn Basics of[ HTML](https://www.w3schools.com/html/html_elements.asp) ?

HTML (Hypertext markup language) is the standard language for web pages. If you want to Scrape data from Web pages, you need to learn HTML.

**The core element of a web page is a text file written in the Hypertext Markup Language (HTML) that describes the content of the web page and includes references to other web resources**.

#### What are HTML Elements and Tags?

HTML tags define the start and end of the HTML Element in a HTML Element.

HTML Element defines the nature of the content written inside it.

Let us say you want to add a heading, we will use **`<h1></h1>`** element.

**`<h1>My Text</h2>`**

Here h1 and h2 are HTML elements.

To understand HTML better, Let us go to Pycharm and create a basic HTML Web Page.

#### Create a HTML File :

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FXhm8rbgGcU6zOwGNt5GV%2Fimage.png?alt=media&#x26;token=59eb073f-ba28-4187-b545-c34a8b8b5bd9" alt=""><figcaption></figcaption></figure>

Delete Eveything written in **`mywebsite`** . Let's Start From Scratch.

#### **`<html> Element :`**

**`<html>`** element is the root element of the html document. It has a starting and ending tag. It contains everything of your website. HTML Document starts with **`<html> element.`**

```python
 <html>

</html>
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FnUa1b2Y70OBd3vxrmNWb%2Fimage.png?alt=media&#x26;token=d552f530-a338-48e8-8b3e-321a3c9151c6" alt=""><figcaption></figcaption></figure>

If you click on Chrome or your desired Browser, A Website will open like this:

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FXCfI4TOc8UuAozn9aaeX%2Fimage.png?alt=media&#x26;token=3239b63e-6cfa-4b7b-b576-5e930089e365" alt=""><figcaption></figcaption></figure>

#### `<head> Element :`

The `<head>` element contains **meta information** about the HTML page`.`

```python
<html>
  <head>
    
  </head>

</html>
```

#### `<title> Element :`

The title element contains title of the website.

```python
<html>
  <head>
    <title>
      E - Commerce Website
    </title>

  </head>

</html>
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FthVCasjZaZtCATT87Gm3%2Fimage.png?alt=media&#x26;token=a7bbd436-071f-4e4f-8037-2d6dba67155e" alt=""><figcaption></figcaption></figure>

#### `<div> Element:`

The \<div> tag **defines a division or a section in an HTML document**. The \<div> tag is used as a container for HTML elements`.`

#### `class Attribute :`

class attribute is used to group a particular section.

Let us say we want to create a post about a phone , we should post a phone for our Website. Yay!!

```python
<html>
  <head>
    <title>
      E - Commerce Website
    </title>

  </head>
  
  <div class="Phone">
    
  </div>

</html>
```

#### `Heading - Add Phone Name`

### `h1 is the most important heading`

#### `h2 is the second important heading`

{% hint style="info" %}
**`h1 is the largest heading and h6 is the smallest one.`**
{% endhint %}

```python
<html>
  <head>
    <title>
      E - Commerce Website
    </title>

  </head>

  <div class="Phone">
    <h1>Samsung Galaxy</h1>

  </div>

</html>
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2F7oZaq5Urk0Pjuyyu8Qzc%2Fimage.png?alt=media&#x26;token=c5eb00fe-f8fe-4b11-a179-5df935fe7cb8" alt=""><figcaption></figcaption></figure>

#### `Image - Add Image of Phone`

Let us say , we want to add a new image for the phone. You can simply use **`<img>`** tag with its `src` attribute containing url or path for the image.

```python
<html>
  <head>
    <title>
      E - Commerce Website
    </title>

  </head>

  <div class="Phone">
    <h1>Samsung Galaxy</h1>
    <img src="https://rukminim1.flixcart.com/image/312/312/l4n2oi80/mobile/x/o/a/-original-imagfhu75eupxyft.jpeg?q=70">
  </div>

</html>
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FLUi0gY32G3j05VczftuK%2Fimage.png?alt=media&#x26;token=e8b5c08b-d1d0-42f0-a430-b21835e5934c" alt=""><figcaption></figcaption></figure>

#### `List - Add Specifications`

There are two kind of list tags.

* [x] `Ordered List <ol>`
* [x] `Unordered List <ul>`

{% tabs %}
{% tab title="Ordered List" %}
1. **6000 mAh Lithium Ion Battery**
2. **50MP + 5MP + 2MP | 8MP Front Camera**
3. **16.76 cm (6.6 inch) Full HD+ Display**
{% endtab %}

{% tab title="Unordered list" %}
* **16.76 cm (6.6 inch) Full HD+ Display**
* **50MP + 5MP + 2MP | 8MP Front Camera**
* **6000 mAh Lithium Ion Battery**
{% endtab %}
{% endtabs %}

```python
<html>
  <head>
    <title>
      E - Commerce Website
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
  </div>

</html>
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2F5Y1ukkRhkDY1EkFaCX80%2Fimage.png?alt=media&#x26;token=4d4c3782-1b33-44c6-a409-8c72141aafe4" alt=""><figcaption></figcaption></figure>

#### `<a> tag - Link To Read More :`

We use `<a>` tag for link and `<href>` attribute for hyperlink.

```python
<html>
  <head>
    <title>
      E - Commerce Website
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

</html>
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2F7jPA0rue8MvVCXHtkbHI%2Fimage.png?alt=media&#x26;token=2a5a1101-ab54-4d17-b0d9-2a0438bde468" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Let us create multiple post for different phone by simply using our `<div class = "Phone"> tag.`
{% endhint %}

#### Adding Three different Phone Posts with same class "Phone" :

```python
<html>
  <head>
    <title>
      E - Commerce Website
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

</html>
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FXRpKAgkCm15Hq6BTkcos%2Fimage.png?alt=media&#x26;token=188b086d-7cd6-46ab-8a9a-0b0c3ac11d9a" alt=""><figcaption></figcaption></figure>

#### Adding Two different Laptop Posts with class "Laptop" :

```python
<html>
  <head>
    <title>
      E - Commerce Website
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


</html>
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FNOqMTERiaa7PC4NRQOC7%2Fimage.png?alt=media&#x26;token=c356e502-afdd-4841-ba07-39d2392994cc" alt=""><figcaption></figcaption></figure>
