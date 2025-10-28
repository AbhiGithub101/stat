# Flipkart Web Scraping

## Flipkart Web Scraping : Laptop

Suppose Big Bazaar wants to move to E-commerce industry and wants to collect data of multiple products from flipkart. Let us start with the collection of laptops data from flipkart.

#### Data to collect :

* [x] **`Product Model`**
* [x] **`Name of the product`**
* [x] **`Price of the Product`**
* [x] **`Link of the Product`**

### Step 1 : Get Html document of the Webpage.

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FdbezTeDX4LVZfS1wEz1E%2Fimage.png?alt=media&#x26;token=4a40c56f-d668-4c63-b14b-076e2e88cc1e" alt=""><figcaption></figcaption></figure>

#### Introduction to requests:

**Requests** allow you to send HTTP requests extremely easily. HTTP (Hypertext transfer protocol) request is used to send requests to the server and access information.

**When a search engine or website visitor makes a request to a web server, a three digit HTTP Response Status Code is returned**. This code indicates what is about to happen. A response code of 200 means "OK, here is the content you were asking for. It means the request is accepted.

To understand more about response codes :

```python
from bs4 import BeautifulSoup
import requests

url = 'https://www.flipkart.com/search?q=laptop&sid=6bo%2Cb5g&as=on&as-show=on&otracker=AS_QueryStore_OrganicAutoSuggest_2_2_na_na_na&otracker1=AS_QueryStore_OrganicAutoSuggest_2_2_na_na_na&as-pos=2&as-type=RECENT&suggestionId=laptop%7CLaptops&requestId=483bcb46-7458-4c48-869c-773583f9e774&as-searchtext=laptop'

response = requests.get(url)

print(response.status_code)

Output : 
200
```

{% hint style="info" %}
If the status\_code is 200, request is succeeded. Most common status code is 200. if the request is succeded , we can get the HTML Document of the web page and start scraping.
{% endhint %}

#### Let the Scraping Begins :

**1. Go to flipkart.com and search for laptop and copy the web page url.**

So first thing that we need to do is to import all necessary libraries and then send a HTTP request to our website and if the request is succeeded , we can access to the html text of the particular web page for scraping.

```python
# Importing necessary Libraries 

from bs4 import BeautifulSoup
import requests

# url of the webpage

url = "https://www.flipkart.com/search?q=laptop&sid=6bo%2Cb5g&as=on&as-show=on&otracker=AS_QueryStore_OrganicAutoSuggest_2_2_na_na_na&otracker1=AS_QueryStore_OrganicAutoSuggest_2_2_na_na_na&as-pos=2&as-type=RECENT&suggestionId=laptop%7CLaptops&requestId=483bcb46-7458-4c48-869c-773583f9e774&as-searchtext=laptop"

# sending HTTP Request to the website and get the response 

response = requests.get(url) 

# if response code is 200, get content of Webpage using content property.

if(response.status_code == 200):
    html_text = response.content 
    print(html_text)
    

Output : 

<!doctype html><html lang="en"><head>
<link href="https://rukminim1.flixcart.com" rel="preconnect"/>
<link rel="stylesheet" href="//static-assets-web.flixcart.com/fk-p-linchpin-web/fk-cp-zion/css/app_modules.chunk.905c37.css"/>
<link rel="stylesheet" href="//static-assets-web.flixcart.com/fk-p-linchpin-web/fk-cp-zion/css/app.chunk.104e9a.css"/>
<meta http-equiv="Content.........
.................</html>

```

#### 2. Converting HTML text into BeautifulSoup

```python
soup = BeautifulSoup(html_text , "lxml")
print(soup.prettify())
```

**Now what are we going to scrape ?**

* [x] **Laptop Model**
* [x] **Laptop Name**
* [x] **Price**
* [x] **Link of the post**
* [x] **Link of the image**
* [x] **Specifications of the laptop**
* [x] **Rating**

#### Scraping first post of the laptop :

If we need to scrape laptops details, we need to scrape first instance of the laptop or first post. If we can scrape first post , we can use that post as anchor and scrape information for all the laptops.

As we have learned previously, same kind of data lies in same class. So let us find class for our Laptop post.

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2F3Zs1fSUAwmD2cfvk5IfW%2Fimage.png?alt=media&#x26;token=738799d9-bccc-42f2-bbc9-3247d02f44bb" alt=""><figcaption></figcaption></figure>

As you can see, all of the contents of our laptop is in **`<a>`** tag, with class name `_1fQZEK` , So let's scrape this.

#### Scraping Laptop Details using `<a>` tag :

```python
laptop = soup.find('a',"_1fQZEK")
print(laptop)
```

Now that we have scraped our Laptop post, let's scrape other details.

#### Scraping Laptop Model :

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FzCNQ3FM5nSIN1qm5a7Fo%2Fimage.png?alt=media&#x26;token=55bb6263-146c-4e44-9e2f-97e2344cf26e" alt=""><figcaption></figcaption></figure>

So the tag name is `<div>` class name for the model is `_4rR01T.`

```python
model = laptop.find('div','_4rR01T').get_text()
print(model)

Output: 

acer Aspire 3 Dual Core 3020e - (4 GB/256 GB SSD/Windows 11 Home) A314-22 Laptop

```

#### Scraping Laptop Brand :

Don't you think we can get Laptop brand from the Model itself by splitting the string using index number to get the laptop name.

```python
brand = model.split(' ')[0].title()
print(brand)

Output : 

Acer
```

#### Scraping Price of the Product :

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FUMMCYdRkvXIKSvjdEROM%2Fimage.png?alt=media&#x26;token=ab468c3c-eef7-4a5f-b25f-12655adb92c1" alt=""><figcaption></figcaption></figure>

You can scrape price from `<div>` tag with class name `<_30jeq3 _1_WHN1>` .

```python
price = laptop.find('div', "_30jeq3 _1_WHN1")
print(price)

Output : 

₹24,990
```

{% hint style="info" %}
But type of price is string instead of integer, so we need to convert it into integer and for that we need to replace unnecessary characters.
{% endhint %}

```python
price = int(phone.find('div', "_30jeq3 _1_WHN1").replace('₹','').replace(',',''))
print(price)

Output : 

24990
```

#### Scraping Link of the laptop :

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FLXsxJjfjahPFUVv2pozu%2Fimage.png?alt=media&#x26;token=138c6c77-e7fd-4401-9bc6-8df162d588fe" alt=""><figcaption></figcaption></figure>

We can get the `<href>` attribute from the a tag `<a>` . But we had already scraped this part and assigned it to the variable lapto&#x70;**.**

```python
link =  "https://www.flipkart.com" + phone['href']
print(link)

Output:

https://www.flipkart.com/acer-aspire-3-dual-core-3020e-4-gb-256-gb-ssd-windows-11-home-a314-22-laptop/p/itm07e718a865608?pid=COMGBNUMF8CDJZFH&lid=LSTCOMGBNUMF8CDJZFHVNFSHE&marketplace=FLIPKART&q=acer&store=6bo%2Fb5g&srno=s_1_6&otracker=search&otracker1=search&fm=organic&iid=ad76d4cc-ba93-4913-b04e-889d6cfb5f9c.COMGBNUMF8CDJZFH.SEARCH&ppt=hp&ppn=homepage&ssid=a2vg4ctgsg0000001664870452054&qH=e4721cdedd884fee
```

Before moving ahead , let us combine everything that we have done by now.

```python
from bs4 import BeautifulSoup
import requests

url = "https://www.flipkart.com/search?q=laptop&sid=6bo%2Cb5g&as=on&as-show=on&otracker=AS_QueryStore_OrganicAutoSuggest_1_2_na_na_na&otracker1=AS_QueryStore_OrganicAutoSuggest_1_2_na_na_na&as-pos=1&as-type=HISTORY&suggestionId=laptop%7CLaptops&requestId=483bcb46-7458-4c48-869c-773583f9e774&as-backfill=on"

response = requests.get(url)

if(response.status_code==200):
    html_text = response.content
    soup = BeautifulSoup(html_text,"lxml")
    laptop = soup.find('a',"_1fQZEK")
    model = laptop.find('div','_4rR01T').get_text()
    brand = model.split(' ')[0].title()
    price = int(laptop.find('div','_30jeq3').get_text().replace('₹','').replace(',',''))
    link =  "https://www.flipkart.com" + laptop['href']
    print(f'''Brand : {brand}
Model : {model}
Price : {price}
Link : {link}''')


Output : 

Brand : Acer
Model : acer Aspire 3 Dual Core 3020e - (4 GB/256 GB SSD/Windows 11 Home) A314-22 Laptop
Price : 24990
Link : https://www.flipkart.com/acer-aspire-3-dual-core-3020e-4-gb-256-gb-ssd-windows-11-home-a314-22-laptop/p/itm07e718a865608?pid=COMGBNUMF8CDJZFH&lid=LSTCOMGBNUMF8CDJZFHVNFSHE&marketplace=FLIPKART&q=acer&store=6bo%2Fb5g&srno=s_1_6&otracker=search&otracker1=search&fm=organic&iid=ad76d4cc-ba93-4913-b04e-889d6cfb5f9c.COMGBNUMF8CDJZFH.SEARCH&ppt=hp&ppn=homepage&ssid=a2vg4ctgsg0000001664870452054&qH=e4721cdedd884fee
```

#### Scraping Link of the image :

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FGS8LqA7hEEkFrAu6VWbZ%2Fimage.png?alt=media&#x26;token=7d975b5a-6c43-479f-9e38-1e7174d48102" alt=""><figcaption></figcaption></figure>

```python
image = laptop.find('img')['src']
print(image)

Output : 

https://rukminim1.flixcart.com/image/312/312/kp2y2kw0/computer/y/0/c/na-thin-and-light-laptop-asus-original-imag3ebnzawky4kn.jpeg?q=70
```

#### Specifications of the laptop :

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FShTof9vme5UqTjpYUe8B%2Fimage.png?alt=media&#x26;token=031f4f96-a870-4506-a457-2760987f0926" alt=""><figcaption></figcaption></figure>

To scrape this we need to follow these steps :

* [x] **Scrape `<ul>` tag.**
* [x] **Scrape all \<li> tag from the \<ul> tag.**
* [x] **Store all specifications in a list.**

```python
specification_list = []
lists = laptop.find('ul')
specifications = lists.find_all('li')
for specification in specifications:
    specification_list.append(specification.get_text())
print(specification_list)

Output : 

['AMD Dual Core Processor', 
'4 GB DDR4 RAM', 
'64 bit Windows 11 Operating System', 
'256 GB SSD', 
'35.56 cm (14 Inch) Display', 
'Acer Care Center, 
Quick Access, 
Acer Product Registration', 
'1 Year International Travelers Warranty (ITW)']

```

#### Scraping Rating from the product :

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2F9wG9attQF6eAaQS4eybt%2Fimage.png?alt=media&#x26;token=dc786d43-be25-4001-ab0c-034e398afb26" alt=""><figcaption></figcaption></figure>

```python
rating = float(laptop.find('div','_3LWZlK').get_text())
print(rating)

Output : 

4.0
```

{% hint style="info" %}
Now that we have Scraped everything , let us combine everything and see the result.
{% endhint %}

```python
from bs4 import BeautifulSoup
import requests

url = "https://www.flipkart.com/search?q=laptop&sid=6bo%2Cb5g&as=on&as-show=on&otracker=AS_QueryStore_OrganicAutoSuggest_1_2_na_na_na&otracker1=AS_QueryStore_OrganicAutoSuggest_1_2_na_na_na&as-pos=1&as-type=HISTORY&suggestionId=laptop%7CLaptops&requestId=483bcb46-7458-4c48-869c-773583f9e774&as-backfill=on"

response = requests.get(url)

if(response.status_code==200):
    html_text = response.content
    soup = BeautifulSoup(html_text,"lxml")
    laptop = soup.find('a',"_1fQZEK")
    model = laptop.find('div','_4rR01T').get_text()
    brand = model.split(' ')[0].title()
    price = int(laptop.find('div','_30jeq3').get_text().replace('₹','').replace(',',''))
    link =  "https://www.flipkart.com" + laptop['href']
    image = laptop.find('img')['src']
    specification_list = []
    lists = laptop.find('ul')
    specifications = lists.find_all('li')
    for specification in specifications:
        specification_list.append(specification.get_text())
    rating = float(laptop.find('div', '_3LWZlK').get_text())
    print(f'''Brand : {brand}
Price : {price}
Link : {link}
Image Link : {image}
Rating : {rating}
Specifications : {specification_list}''')


Output : 

Brand : Acer
Price : 21890
Link : https://www.flipkart.com/acer-aspire-3-dual-core-3020e-4-gb-256-gb-ssd-windows-11-home-a314-22-laptop/p/itm07e718a865608?pid=COMGBNUMF8CDJZFH&lid=LSTCOMGBNUMF8CDJZFHVNFSHE&marketplace=FLIPKART&q=laptop&store=6bo%2Fb5g&srno=s_1_1&otracker=AS_QueryStore_OrganicAutoSuggest_1_2_na_na_na&otracker1=AS_QueryStore_OrganicAutoSuggest_1_2_na_na_na&fm=organic&iid=en_Gbo3777pGH7PAcF2H26oAIXyFRd0RPuu3u9xDpwameJZkT0HUiVYAfbkaioxeA9TFXuZ9FCqywavLb%2B8qN9sag%3D%3D&ppt=None&ppn=None&ssid=7yr62k7ir40000001664969271008&qH=312f91285e048e09
Image Link : https://rukminim1.flixcart.com/image/312/312/xif0q/computer/h/u/b/-original-imagg2vnsrgrfkmz.jpeg?q=70
Rating : 4.0
Specifications : 
['AMD Dual Core Processor', 
'4 GB DDR4 RAM', 
'64 bit Windows 11 Operating System', 
'256 GB SSD', '35.56 cm (14 Inch) Display', 
'Acer Care Center, 
Quick Access, 
Acer Product Registration', 
'1 Year International Travelers Warranty (ITW)']

```

<details>

<summary>Section 2</summary>

* **We will scrape details of all the phones**
* **Create a Dictionary to store all the details.**

</details>

#### Scrape details of all the Laptops in our current Web page :

We have scraped a single Laptops detail , now if we want to scrape details of all the Laptops all we need to do is to find all the occurences of `<a>` tag with class name `<_1fQZEK>.`

Doing this is pretty simple.All you need to do is to use `<find_all>` , Like this :

```python
laptops = soup.find_all('a','_1fQZEK')
for laptop in laptops : 
    # use above written script for single laptop data scraping 
```

Like this :

```
from bs4 import BeautifulSoup
import requests

url = "https://www.flipkart.com/search?q=laptop&sid=6bo%2Cb5g&as=on&as-show=on&otracker=AS_QueryStore_OrganicAutoSuggest_1_2_na_na_na&otracker1=AS_QueryStore_OrganicAutoSuggest_1_2_na_na_na&as-pos=1&as-type=HISTORY&suggestionId=laptop%7CLaptops&requestId=483bcb46-7458-4c48-869c-773583f9e774&as-backfill=on"

response = requests.get(url)

if(response.status_code==200):
    html_text = response.content
    soup = BeautifulSoup(html_text,"lxml")
    laptops = soup.find_all('a',"_1fQZEK")
    for laptop in laptops:
        model = laptop.find('div','_4rR01T').get_text()
        brand = model.split(' ')[0].title()
        price = int(laptop.find('div','_30jeq3').get_text().replace('₹','').replace(',',''))
        link =  "https://www.flipkart.com" + laptop['href']
        image = laptop.find('img')['src']
        specification_list = []
        lists = laptop.find('ul')
        specifications = lists.find_all('li')
        for specification in specifications:
            specification_list.append(specification.get_text())
        rating = float(laptop.find('div', '_3LWZlK').get_text())
        print(f'''Brand : {brand}
    Price : {price}
    Link : {link}
    Image Link : {image}
    Rating : {rating}
    Specifications : {specification_list}''')
```
