# Data Collection Through APIs

#### <mark style="color:purple;">Let's Understand the Problem :</mark>

let's imagine a scenario where you are sitting at a restaurant and want to order a meal. In this scenario, the waiter acts as the API.

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FIN62dqIqXxmTrxcDK0Sm%2FE-Commerce.png?alt=media&#x26;token=398eaf24-387a-4a51-b90d-bf0493c81521" alt=""><figcaption></figcaption></figure>

The waiter (API) serves as an intermediary between you (the client) and the chef (the server). You, as the client, don't directly communicate with the chef; instead, you communicate your order to the waiter, who then takes it to the chef and returns the prepared meal to you.

In this analogy, the waiter represents the API, and the chef represents the server or the backend system providing the requested service or data.

Let's say you want to book a trip with your friends and you go to website MakeMyTrip. Now you can easily see all the scheduled trains , and pay for the ticket. But how is it possible? Obviously IRCTC would not share its whole data with MakeMyTrip. Right ?

When you search for a flight on MakeMyTrip, they use their own website to show you the results. But behind the scenes, they might use their API to get flight information from airlines and show it to you. The API allows MakeMyTrip to get the necessary data from the airlines and display it on their website in a nice format.

Similarly, let's say you want to book a train ticket and you go to the IRCTC website. IRCTC is a website for booking train tickets in India. They also have an API that allows other websites or apps to access their train ticket information.

When you search for a train on the IRCTC website, they use their own website to show you the available trains and ticket details. But again, behind the scenes, they might use their API to get the train information from the Indian Railways and display it on their website.

So, in simple terms, an API is like a special language that allows different websites or apps to talk to each other and share information. It helps websites like MakeMyTrip and IRCTC get the data they need from airlines or Indian Railways, and present it to you in a way that you can easily understand and use to plan your trips.

#### Introduction

This documentation provides a comprehensive guide on how to collect data using an API (Application Programming Interface). It aims to explain the key concepts, methods, and steps required to successfully retrieve data from an API.

#### Table of Contents

1. What is an API?
2. Choosing an API
3. API Key and Authentication
4. Making API Requests
5. Handling Responses
6. Pagination
7. Rate Limiting
8. Error Handling
9. Data Transformation and Storage
10. Conclusion

#### 1. What is an API?

An API is a set of rules and protocols that allows different software applications to communicate and interact with each other. It defines the methods and data formats that developers can use to request and receive information from a service or platform.

In the context of data collection, an API enables you to retrieve data from a remote server or service programmatically, without having to manually access and scrape web pages.

#### 2. Choosing an API

When collecting data using an API, you need to choose the appropriate API for your specific needs. Consider the following factors:

* **Data Source**: Identify the platform or service that provides the data you require. Common examples include social media platforms (Twitter, Facebook), weather services, financial data providers, etc.
* **API Documentation**: Review the API documentation provided by the data source. It should outline the available endpoints, parameters, authentication methods, and response formats.
* **Data Availability**: Ensure that the required data is accessible through the API. Some APIs might have restrictions on certain types of data or require additional permissions.

#### 3. API Key and Authentication

Many APIs require authentication to ensure that only authorized users can access the data. Typically, this involves obtaining an API key, which serves as a unique identifier for your application.

Follow these steps to authenticate with an API:

* Sign up or create an account with the data source.
* Generate an API key associated with your account.
* Include the API key in your API requests as a parameter or in the request headers, as specified in the API documentation.

#### 4. Making API Requests

API requests are HTTP-based and can be made using various programming languages. The most common methods for making API requests are:

* **GET**: Retrieves data from the API.
* **POST**: Submits data to the API.
* **PUT**: Updates existing data in the API.
* **DELETE**: Removes data from the API.

#### 5. Handling Responses

API responses are typically returned in a structured format, such as JSON (JavaScript Object Notation) or XML (eXtensible Markup Language). JSON is widely used and easy to work with in most programming languages.

Once you receive an API response, you can parse the data and extract the relevant information for further processing or storage.

#### 6. Pagination

If the API's response contains a large amount of data, it may be paginated to improve performance. Pagination allows you to retrieve data in chunks or pages.

The API documentation should specify the pagination parameters, such as the page size and how to navigate through the pages using parameters like "page" or "offset".

Iterate through the pages until you have retrieved all the required data.

#### 7. Rate Limiting

To prevent abuse or overloading of their servers, APIs often enforce rate limits. Rate limiting restricts the number of API requests you can make within a certain time frame.

Check the API documentation for the rate limit details, such as the maximum number of requests allowed per minute or hour.

#### <mark style="color:purple;">Let's Dive in</mark> :

We all know IMDB (Internet Movie Database). Suppose you want to collect Data of Top Rated Movies from IMDB. Now Collecting Data manually from IMDB is tedious task if you are doing it manually. But If we could get access to it's API, We can simply fetch data by using python and few libraries.

1. **Sign up for an API key**: Go to [https://imdb-api.com/](https://imdb-api.com/) and sign up for an account. Once registered, you should be provided with an API key. Keep this key handy, as you will need it to authenticate your API requests.

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FWg9lhKHibLr58BkaMnDB%2Fimage.png?alt=media&#x26;token=66df7e38-d332-4cf1-a66e-c11c13f69aa0" alt=""><figcaption></figcaption></figure>

Now go to API and you will find your API KEY.

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2F4myOkBRKklc586f46MJf%2Fimage.png?alt=media&#x26;token=9d3f3d59-3e3e-466e-b915-0cb4a328be69" alt=""><figcaption></figcaption></figure>

An API key is a unique identifier or access token that allows you to authenticate and authorize your access to an API (Application Programming Interface). It serves as a security measure to ensure that only authorized users or applications can make requests to the API and retrieve the desired data.

Here are the primary uses of an API key:

1. **Authentication**: The API key acts as a credential that verifies your identity and authorizes your access to the API. By including the API key in your API requests, you demonstrate that you have the necessary permissions to interact with the API's resources.
2. **Access Control**: APIs often provide different levels of access or functionality based on the user's role or subscription. The API key helps determine the level of access you have, allowing the API provider to enforce restrictions or limitations as needed.
3.
4. **Usage Tracking and Billing**: API keys enable the API provider to track usage and monitor how their service is being utilized. It allows them to measure the number of requests, manage quotas or rate limits, and potentially apply usage-based billing if applicable.
5. **Security and Protection**: API keys help protect the API and its resources from unauthorized access or abuse. By requiring an API key, the provider can monitor and control the usage of their API, mitigate potential security risks, and revoke access if needed.
6. **Developer Identification**: For APIs that are open to third-party developers, each developer or application is typically assigned a unique API key. This key can be used to identify and track the specific developer or application responsible for making API requests.

**Choose the data you want to collect**: Determine the specific data you wish to collect from IMDB. For example, you might be interested in retrieving movie details, actor information, or user reviews. Identify the appropriate API endpoint that provides the desired data.

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FRuTwJ85wHhpcFz5w6EN8%2Fimage.png?alt=media&#x26;token=71e56d1c-9187-4f37-be36-4209ed3f0e00" alt=""><figcaption></figcaption></figure>

you can choose any API. I am going with Most Popular Movies. As You can see below Test , There is a link where we can get Data of most Popular movies.

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FAVaZEu01HetvHPs10xOX%2Fimage.png?alt=media&#x26;token=92d614ef-fc3f-4728-8440-f68fa05c6953" alt=""><figcaption></figcaption></figure>

1. `import pandas as pd`: This line imports the Pandas library, which provides data manipulation and analysis tools for Python. It is commonly used for working with tabular data.
2. `import requests`: This line imports the Requests library, which allows you to send HTTP requests and handle responses in Python. It is commonly used for interacting with APIs.

```python
import pandas as pd 
import requests
```

1. `url = 'https://imdb-api.com/en/API/MostPopularMovies/k_y8d174d2'`: This line assigns the URL of the API endpoint to the variable api. The URL points to the IMDb API endpoint that provides a list of most popular movies.

```python
api = 'https://imdb-api.com/en/API/MostPopularMovies/k_y8d174d2'
```

1. `data = requests.get(api).json()`: This line sends a GET request to the API endpoint specified by the api variable using the `requests.get()` function. It retrieves the response from the API, and the `.json()` method is called on the response to convert it into a Python dictionary format. The resulting data is assigned to the variable `data`.

```python
data = requests.get(api).json()
```

1.
2. `data = data['items']`: This line extracts the value associated with the key 'items' from the `data` dictionary and reassigns it to the `data` variable. This step assumes that the API response contains a key called 'items' that holds the relevant movie data.

```python
data = data['items']
```

1. `df = pd.json_normalize(data)`: This line uses the `pd.json_normalize()` function from the Pandas library to convert the nested JSON data (list of dictionaries) in the `data` variable into a tabular format. It creates a DataFrame, which is a two-dimensional table-like data structure in Pandas, and assigns it to the variable `df`.

```python
df = pd.json_normalize(data)
```

1. `df.to_csv('MostPopularMovies.csv')`: This line saves the DataFrame `df` as a CSV (Comma-Separated Values) file named 'MostPopularMovies.csv' using the `.to_csv()` method. The resulting CSV file will contain the tabular data from the DataFrame, with each row representing a movie and each column representing a movie attribute.

```python
df.to_csv('MostPopularMovies.csv')
```

<figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FnNcWje7Tazc6lxSB24fl%2Fimage.png?alt=media&#x26;token=8c81d80c-520e-4417-af94-0751716c4b3d" alt=""><figcaption></figcaption></figure>
