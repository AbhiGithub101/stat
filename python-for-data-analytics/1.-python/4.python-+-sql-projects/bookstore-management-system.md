# Bookstore Management System

## Bookstore Management System

In this project we are going to see how we can create a Bookstore Management System using **Python** and **MySQL.**

#### A Bookstore Management System is a computer-based system that is used to manage and keep track of the inventory, orders, and sales of a bookstore. It is typically used by bookstores that maintain a large inventory of books and other related items.

### <mark style="color:purple;">Scenario</mark>

#### **This program will be directly used by the store owner, where he will be manually adding the book details and whichever customer is coming for purchasing the book, the owner will be adding customer details along with the book's ISBN Number which the customer purchased. This is the whole scenario of this project.**

In this project we will see a console based application through which we can store **books, take orders from customers, store customer details** and **calculate total sales.** Other than this, we will be able to view all the books details, update and delete the books, alongside, we can view all the customers as well.

In addition to this a login credentials for admin has been provided but there is no option for user to be created it is being directly maintained by the **Database Administrator**.

So here is a list of tasks we will perform in the above projects.

* [x] Installation of **mysql connector**
* [x] **Importing the module mysql.connector**
* [x] **Connecting to MySQL using MySQL Credentials.**
* [x] Addition of Books details along with its price
* [x] Updation of book details(price only).
* [x] Deletion of Book using it's _**ISBN**_ Number
* [x] Searching of Book on the basis of different conditions.
* [x] Viewing All the Books
* [x] Addition of Customer for if he buys a book
* [x] Viewing the details of all the customers.
* [x] **Tables** and **database** in **MySQL** used in this project
* [x] Creation of Tables and Databases.

#### **Installation of MySQL Connector**

**First Step, Install the MySQL connector you can install it using either**

1.  **Right** clicking on the windows icon and select windows powershell and on windows powershell prompt. Type--->

    `pip install mysql-connector-python`\
    \
    It will be installed directly into the _**site packages**_ folder of your python and due to this you will be able to use it anywhere in any IDE using the python installed in your windows.
2. Or using PyCharm follow these steps to install the _**mysql-connector-python**_
   1. _**Click on File**_
   2. _Click on settings_
   3. _Click on Project --> Python Interpreter_
   4. _Click on + button on left side_
   5. _On Search Bar Type_ **mysql-connector-python**
   6. **Install it**

See the Images

<div><figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FB5BotI6EDSfipKEyKO6I%2FScreenshot%20(159).png?alt=media&#x26;token=26ae37c2-52d7-444f-8f99-872834e38990" alt=""><figcaption></figcaption></figure> <figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FxgoYjcLfrrzzJCXtxfHK%2FScreenshot%20(160).png?alt=media&#x26;token=ad791a74-eceb-4c6e-9d7c-0d55ddffd2f7" alt=""><figcaption></figcaption></figure> <figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FWeUrQT75qdqdfqbd4yZn%2FScreenshot%20(161).png?alt=media&#x26;token=87b2e517-333b-4544-9f8d-29cc1d5fd563" alt=""><figcaption></figcaption></figure> <figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FPp8IaaPNt1UjPFy6WJsG%2FScreenshot%20(162).png?alt=media&#x26;token=62b38460-537d-403a-be72-4da7b07080db" alt=""><figcaption></figcaption></figure></div>

#### Importing the Module **mysql.connector**

```python
import mysql.connector as sql

#Importing mysql.connector with an alias name sql for connecting to mysql
```

#### Connecting to **MySQL using MySQL Credentials**

```python
import mysql.connector as sql

# Establishing Connection to my sql using mysql credentials
con = sql.connect(host='localhost', user='root', password='', database='book_store')
# obtaining the cursor
cur = con.cursor()
```

\
**Here, in host if you are using mysql in your local machine provide localhost as the host and in user and password provide your MySQL username and password to login into the MySQL and in database provide the database in which you want to work. This may be of different name for different people. (Before doing this, ensure your MySQL is working either through MySQL workbench, xampp or wamp).**

#### **Creation of Database and Tables in MySQL**

**`1.`**`create database book_store`\
\
\&#xNAN;**`2.`**` `` ``use book_store `\
\
\&#xNAN;**`3.`**` `` ``create table login_book(userid varchar(20) primary key, password varchar(20) unique) `\
\
\&#xNAN;**`4.`**` `` ``create table books(isbn bigint primary key, title varchar(100), author varchar(100), publisher varchar(100), price int, quantity_sold int, total_sales int) `\
\
\&#xNAN;**`5.`**` `` ``create table cust_purchase(cust_id int primary key auto_increment, cname varchar(30), cphone bigint(10), isbn bigint, foreign key(isbn) references books(isbn)) `

#### Tables and Databases used in the project

**There are two tables used :**\
**1. login\_book for login into the system**\
**2. books for storing the book details.**\
**3. cust\_purchase for storing the customer details.**

#### **Start of the program**

The program starts from a main() function asking the user for the credentials to verify and log into the system.\
\
The function written below is **main()** and it takes userid and password as input from the user(This userid and password input from user is totally different from what we created in above table).\
\
Then these credentials are verified and if user id is wrong then message for userid is shown while if password is wrong message for wrong password is shown to the user.\
\
Here is the function,\\

```python
def main():
    print('---------------Enter Your Credentials to Login-----------------')
    #Taking userid and password input from the user
    userid = input('Enter your user id : ')
    password = input('Enter your password : ')
    #Executing Queries
    query = 'SELECT * FROM LOGIN_BOOK'
    cur.execute(query)
    #Iterating over the records fetched
    for det in cur.fetchall():
        if userid == det[0]: # checking for if userid is same as we give
            if password == det[1]: # checks if password for the userid is correct or not
                start(userid) #if all true then start the system using start method
            else:
                print(f'Wrong Password for {userid}')
            break
    else:
        print(f'Wrong userid, \nuserid {userid} doesn\'t exists')

main()
```

The **SQL Query** used for validating the **userid** is\
\&#xNAN;**`SELECT * FROM LOGIN_BOOK`**\
\
The module **mysql.connector** contains a function _**execute(query)**_ where we have to pass our query and this function will execute your query in the database. This function can be accessed using the reference of cursor such as **cur here is used to execute the query.**\
\
Inside this function you can write your query in two ways -\
`1. query = "select * from login_book"`\
`cur.execute(query)`

Using above method we can create our query in a string and then we can pass that string of query to the execute function.\
\
`2. cur.execute("select * from login_book")`\
\
You can directly pass your query also.\
\
So this main() function will validate your identity and if it is correct then it will call the method **start(userid).**\
\&#xNAN;_start(userid) function is the point where all the system starts, here userid is a parameter passed in which the userid you entered which is validated with the database is sent to show in case of log out from the system._\
\
\&#xNAN;_**Now we define start(userid) function, here is the code:**_

```python
def start(userid):
#Infinite Loop to start execution and end when user want
    while True:
        print('MAIN MENU'.center(50,'-')) #Displaying menu to the user.
        print('1. Add Book Details')
        print('2. Update Book Details')
        print('3. View All Books')
        print('4. Delete Book')
        print('5. Search Book')
        print('6. Add Customer Details')
        print('7. View All Customers')
        print('8. Exit') #By providing 5 as input user can log out or exit
        choice = int(input('Enter your choice : '))
        if choice == 1:
            #Choice 1 : add_book() function to add new books
            add_book()
        elif choice == 2:
            #Choice 2 : update_book() function to update a book details(price/qs only).
            update_book()
        elif choice == 3:
            #Choice 3 : view_books() function to view all the books in the store.
            view_books()
        elif choice == 4:
            #Choice 4 : delete_book() function to delete the book specified by ISBN.
            delete_book()
        elif choice == 5:
            #Choice 5: search_book() function to search the book on the basis 
            #of different options.
            search_book()
        elif choice == 6:
            #choice 6: to add customer while the selling of book
            customer_purchase()
        elif choice == 7:
            #choice 7: to view all the customers who purchased all the books.
            view_customers()
        elif choice == 8:
            #Here we have used the role of userid at the time of logout or exit.
            print(f'THANKYOU {userid}'.center(50,'-'))
            break
        else:
            #If user gives value other than 1 to 5 then this message is displayed.
            print('Wrong choice given !!')
            print()

```

Prints a menu to the user asking to enter the choice of operation he want to perform. Sometimes user may enter wrong choice i.e. other than 1 to 8 then a message to display is added in else block.\
On choosing option 8 the elif block contains a break statement which will break the loop and exit the program by showing the userid of the user.

Here is the images,

<div><figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FwVGxLLZJXgMA6D2ya5ik%2FScreenshot%202023-04-03%20164315.jpg?alt=media&#x26;token=46250efc-0816-4b10-90ca-dcd30a992883" alt=""><figcaption><p>main() function starts here</p></figcaption></figure> <figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FVV4gZFm1xK3WWBPIok8E%2FScreenshot%202023-04-04%20154.jpg?alt=media&#x26;token=b6dc4c19-5959-4227-9ea2-9f1de9941ebb" alt=""><figcaption></figcaption></figure></div>

#### Addition of Books (Choice 1)

On choosing the option 1, the program is redirected to function **add\_book()** to add books into the book store. In this **add\_book()** function _**Book ISBN, title, author, publisher and price is entered into the database.**_\
\
\&#xNAN;_Here is the code,_

```python
def add_book():
    global total_sales
    total_sales = 0
    
    quantity_sold = 0 #because we want to initialize the value of quantity_sold to be 0 at the time of addition.
    
    print()
    print('Add Books'.center(30, '*'))
    print('Please Provide Book Details ----->')
    isbn = input('Enter ISBN No.(5 Digits) : ')
    if len(isbn) == 5 and isbn.isdigit():
        title = input('Enter Book Title : ')
        author = input('Enter Book Author : ')
        publisher = input('Enter Book Publisher : ')
        price = int(input('Enter the book price : '))
        
        # Writing Queries
        isbn = int(isbn)
        query = f"insert into books values({isbn}, '{title}', '{author}', '{publisher}', {price}, {quantity_sold}, {total_sales})"
        # Now Executing the query
        cur.execute(query)
        con.commit()
        print('***********Record Inserted Successfully*********')
    else:
        print('>>>>>>Please Provide ISBN Number Correctly <<<<<<<')
    print()
```

Let's have a look into the code above and try to understand -

```python
def add_book():
    global total_sales
    total_sales = 0
    
    quantity_sold = 0 #because we want to initialize the value of quantity_sold to be 0 at the time of addition.
    
    print()
```

**total\_sales** variable is created using **global** keyword because we want to access this keyword everywhere in the program. _**(using global keyword we can either access the global variable of the program or can create a variable that will be declared globally and will be available to all the functions.)**_\
\
**total\_sales** variable is for storing the total sales per day and which will be calculated using -\
\
\&#xNAN;**`total_sales = quantity_sold * price`**\
\
This **total\_sales** will be stored into the database of book\_store in **books** table when a customer is added for any book(in case of purchase).

**Now moving furthur....**

```python
isbn = input('Enter ISBN No.(5 Digits) : ')
```

Here we will take input of **isbn number** from user and will be check on the basis of this and will store into the database.\
\&#xNAN;_The **ISBN** number is taken as a string input because we want to check the length of the isbn number so instead of writing another code for obtaining the number of digits we can simply use strings._

```python
if len(isbn) == 5 and isbn.isdigit():
        title = input('Enter Book Title : ')
        author = input('Enter Book Author : ')
        publisher = input('Enter Book Publisher : ')
        price = int(input('Enter the book price : '))
```

Since we want that **isbn number** must be of **len(**&#x69;sb&#x6E;**)** = 5 and will check whether the user has provided the correct ISBN number of not without '-' . Below, we have taken the neccessary inputs from the user to store into the databases.

Now converting the isbn into an integer value and Writing Query for inserting the record into the database.

```python
 # Writing Queries
        isbn = int(isbn)
        query = f"insert into books values({isbn}, '{title}', '{author}', '{publisher}', {price}, {quantity_sold}, {total_sales})"
        
        # Now Executing the query
        cur.execute(query)
        con.commit()
```

\
**And all the details will be inserted into the MySQL database successfully.**

#### Updating the Book Details(price only)

We will update the **price and quantity sold** details in a book using **isbn** number.\
Through these details total\_sales will be calculated.

Here is the code for **update\_book(),**

```python
def update_book():
    print()
    print('****Update Records*****')
    isbn = int(input('Enter ISBN No. : '))
    query = f"select * from books where isbn = {isbn}"
    cur.execute(query)
    lst = cur.fetchall()

    if len(lst) != 0:
        price = int(input('Enter the new price : '))
        query = f"update books set price = {price} where isbn = {isbn}"
        cur.execute(query)
        con.commit()

        query1 = f"update books set total_sales = price * quantity_sold where isbn = {isbn}"
        cur.execute(query1)
        con.commit()
        print('Record Updated Successfully')
    else:
        print(f'No Book With the ISBN {isbn} provided')
    print('***********************')
    print()

```

Let's have a look into the code and try to understand,

```python
isbn = int(input('Enter ISBN No. : '))
query = f"select * from books where isbn = {isbn}"
cur.execute(query)
```

**ISBN** number is asked to find the record on which update is to be done.

Now Query of MySQL is executed using **cur.execute(query)** function to fetch the record of ISBN Number provided.

In the next step, we check for whether the book with that isbn number is there in database or not. When a book with the **ISBN** number provided is not in the **books** table then an empty list will be returned with no records. Using this, we can check for whether we have any book or not.

```python
 if len(lst) != 0:
        price = int(input('Enter the new price : '))
        query = f"update books set price = {price} where isbn = {isbn}"
        cur.execute(query)
        con.commit()

        query1 = f"update books set total_sales = price * quantity_sold where isbn = {isbn}"
        cur.execute(query1)
        con.commit()
        print('Record Updated Successfully')
    else:
        print(f'No Book With the ISBN {isbn} provided')
```

Now price is asked from user to update the database. Simple UPDATE Query of MySQL is used to update the database.

#### Deletion of Book using it's ISBN Number

If we want to delete our record from our book store then this can be achieved using delete query of **MySQL** here is the code to achieve this,

```python
def delete_book():
    print()
    print("********** DELETE ************")
    isbn = int(input('Enter ISBN No. : '))

    query = f"select * from books where isbn ={isbn}"
    cur.execute(query)

    lst = cur.fetchall()
    if len(lst) != 0:
        try:
            cur.execute(f"delete from books where isbn = {isbn}")
            con.commit()
        except:
            print('Customer Exist with the book purchased')        
    else:
        print(f'No record with ISBN = {isbn}')

    print("******************************")
    print()

```

Taking input of **ISBN** Number to find the record with the matching ISBN Numbered book to delete.

This record will be a list of tuple and therefore is stored into the list for further operation.\
Here **try and except block** is used because we have a relation of **`cust_purchase`** table with **`books` table** using **isbn** number through **Foreign Key**, so there may occur delete anomaly while deleting a book record from database as a customer may exist with that book purchased.

#### Searching of Book on the basis of different conditions

We can perform a search on the basis of different factors such as ISBN Number, Book title, Author Name and Publisher Name.\
\
But it is more preferred to search as per the ISBN Number since records fetched will be unique always in case of searching through ISBN Number.

Here is the code for **search\_book(),**

```python
def search_book():
    print()
    print('Search'.center(30,'-'))
    print('Search on the basis of : ')
    print('1. ISBN Number')
    print('2. Book Title')
    print('3. Author Name')
    print('4. Publisher Name')
    choice = int(input('Enter your choice : '))
    if choice == 1:
        search_value = int(input('Enter ISBN Number(5 Digits) : '))
        cur.execute(f'select * from books where isbn = {search_value}')
        lst = cur.fetchall()
        if len(lst) == 0:
            print('No Book with the ISBN Provided')
        else:
            print('Book Detail : ')
            for book in lst:
                print(book, end='\t')
    elif choice == 2:
        search_value = input('Enter Book Title : ')
        cur.execute(f"select * from books where title = '{search_value}'")
        lst = cur.fetchall()
        if len(lst) == 0:
            print('No Book with the title Provided')
        else:
            print('Book Detail : ')
            for book in lst:
                print(book, end='\t')
    elif choice  == 3:
        search_value = input('Enter the Author Name : ')
        cur.execute(f"select * from books where author = '{search_}'")
        lst = cur.fetchall()
        if len(lst) == 0:
            print('No Book with the author name Provided')
        else:
            print('Book Detail : ')
            for book in lst:
                print(book, end='\t')
    elif choice == 4:
        search_value = input('Enter the Publisher : ')
        cur.execute(f"select * from books where publisher = '{search_value}'")
        lst = cur.fetchall()
        if len(lst) == 0:
            print('No Book with the publisher name Provided')
        else:
            print('Book Detail : ')
            for book in lst:
                print(book, end='\t')
    else:
        print('Wrong Choice Given!!')
    
    print()

```

Above is a very simple Code, using which we can search a book by providing either ISBN number or other things such as author name and all. Like main() for each choice there is an if - elif block.\
\&#xNAN;**`query = "select * from books where isbn = search_value"`**\
**Where search\_value is the value which is used for searching the value, it may be author name or publisher name depending upon on which choice user want to search.**

#### Viewing all the books

All the books can be viewed using the function **view\_books()** here is the code,

```python
def view_books():
    print()
    query = "select * from books"
    cur.execute(query)
    lst = cur.fetchall()
    if len(lst) == 0:
        print('\n---No Books to display----\n')
        return

    print('Displaying Records'.center(150, '-'))
    print("ISBN".center(15), "Title".center(15), "Author".center(15), "Publisher".center(15), "Price".center(15), "Quantity Sold".center(15), "Total Sales".center(15))
    for book in cur.fetchall():
        print(str(book[0]).center(15), book[1].center(15), book[2].center(15), book[3].center(15), str(book[4]).center(15), str(book[5]).center(15), str(book[6]).center(15))
    print("".center(150, '-'))
    print()
```

All the records can be fetched using **`select * from books`**

**Then all the records can be printed in tabular form using some string formatting functions and for loop.**

#### Addition of Customer Details on the time of Book Purchase

While a customer purchase a book, the bookstore owner will add the record of that customer into his database and on the basis of this addition the quantity\_sold and total sales in **`books`** table will be updated.\
Here is the code to achieve this,

```python
def customer_purchase():
    print()
    #Displaying the list of all the books for the operator to add ISBN number on the time of purchase.
    print('Displaying the list of All Books---->')
    query = "select * from books"
    cur.execute(query)

    print("ISBN".center(15), "Title".center(15), "Author".center(15), "Publisher".center(15), "Price".center(15))
    for book in cur.fetchall():
        print(str(book[0]).center(15), book[1].center(15), book[2].center(15), book[3].center(15), str(book[4]).center(15))

    #Now entering the customer details who have purchased the book.
    print()
    cust_name = input('Enter the customer name : ')
    cust_phone = int(input('Enter 10 digit Mobile Number : '))
    isbn = int(input('Enter ISBN : '))
    query = f"insert into cust_purchase(cname, cphone, isbn) values('{cust_name}', {cust_phone}, {isbn})"
    try:
        cur.execute(query)
        con.commit()

        #Join Query + Sub Query
        cur.execute("update books set quantity_sold = (select count(cust_id) from cust_purchase where cust_purchase.isbn = books.isbn)")
        con.commit()

        cur.execute("update books set total_sales = price * quantity_sold")
        con.commit()
        
        print('Customer Added Successfully')
    except sql.Error as err:
        print('No Book with the isbn provided')
    print()


```

Let's try to understand each block of code,

```python
 #Displaying the list of all the books for the operator to add ISBN number on the time of purchase.
 print('Displaying the list of All Books---->')
    query = "select * from books"
    cur.execute(query)

    print("ISBN".center(15), "Title".center(15), "Author".center(15), "Publisher".center(15), "Price".center(15))
    for book in cur.fetchall():
        print(str(book[0]).center(15), book[1].center(15), book[2].center(15), book[3].center(15), str(book[4]).center(15))
```

In this code, we display all the books to the operator for his help to add customer details.

```python
    cust_name = input('Enter the customer name : ')
    cust_phone = int(input('Enter 10 digit Mobile Number : '))
    isbn = int(input('Enter ISBN : '))
    query = f"insert into cust_purchase(cname, cphone, isbn) values('{cust_name}', {cust_phone}, {isbn})"
```

Now appropriate details of customer has been taken and query for adding into the database is written.\
On closer look into the insert query we have not added the cust\_id column declared during the creation of table, it is due to this column is set to auto\_increment and primary key, we don't need to provide any value, it will automatically asign value 1 to the first column and will simply increment on insertion of every next record.

<pre class="language-python"><code class="lang-python"><strong>    try:
</strong>        cur.execute(query)
        con.commit()

        #Join Query + Sub Query
        cur.execute("update books set quantity_sold = (select count(cust_id) from cust_purchase where cust_purchase.isbn = books.isbn)")
        con.commit()

        cur.execute("update books set total_sales = price * quantity_sold")
        con.commit()
        
        print('Customer Added Successfully')
    except sql.Error as err:
        print('No Book with the isbn provided')
    print()
</code></pre>

While executing the query, **try and except** block is used to handle the error when there is no book with the isbn provided due to integrity imposed by foreign key.\
\
In this Query,

```python
cur.execute("update books set quantity_sold = (select count(cust_id) from cust_purchase where cust_purchase.isbn = books.isbn)")
con.commit()
```

We have used join and subquery both to update the quantity\_sold in books table because we want that whenver a customer is added, the system must automatically update the record in the books table such as quantity\_sold and total\_sales.

<div><figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FXU4ezawNUxyasYUyYL1t%2FScreenshot%20(164).png?alt=media&#x26;token=cb72a868-1a9b-45bd-a1f3-5f662da09f24" alt=""><figcaption></figcaption></figure> <figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FR8UWZMIL73tsXHspyc4O%2FScreenshot%20(165).png?alt=media&#x26;token=86ad261c-23f3-4791-be2f-dc792753b5fb" alt=""><figcaption></figcaption></figure> <figure><img src="https://2715416193-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FqrOwR7E0344TGTnSFHoL%2Fuploads%2FKiDWk2O4J4bDTv9fRaBK%2FScreenshot%20(167).png?alt=media&#x26;token=3b9fb615-d65b-4cd1-9ee0-74f2402aa3a2" alt=""><figcaption></figcaption></figure></div>

Above are the images for customer addition and record updation in books table.

<details>

<summary>Full Source Code</summary>

```python
import mysql.connector as sql



# Establishing Connection to my sql using mysql credentials
con = sql.connect(host='localhost', user='root', password='', database='book_store')
# obtaining the cursor
cur = con.cursor()

def customer_purchase():
    print()
    #Displaying the list of all the books for the operator to add ISBN number on the time of purchase.
    print('Displaying the list of All Books---->')
    query = "select * from books"
    cur.execute(query)

    print("ISBN".center(15), "Title".center(15), "Author".center(15), "Publisher".center(15), "Price".center(15))
    for book in cur.fetchall():
        print(str(book[0]).center(15), book[1].center(15), book[2].center(15), book[3].center(15), str(book[4]).center(15))

    #Now entering the customer details who have purchased the book.
    print()
    cust_name = input('Enter the customer name : ')
    cust_phone = int(input('Enter 10 digit Mobile Number : '))
    isbn = int(input('Enter ISBN : '))
    query = f"insert into cust_purchase(cname, cphone, isbn) values('{cust_name}', {cust_phone}, {isbn})"
    try:
        cur.execute(query)
        con.commit()

        #Join Query + Sub Query
        cur.execute("update books set quantity_sold = (select count(cust_id) from cust_purchase where cust_purchase.isbn = books.isbn)")
        con.commit()

        cur.execute("update books set total_sales = price * quantity_sold")
        con.commit()
        
        print('Details Added Successfully')
    except sql.Error as err:
        print('No Book with the isbn provided')
    print()


def view_customers():
    print('Displaying Records'.center(150, '-'))
    query = "select * from cust_purchase"
    cur.execute(query)

    print("Customer ID".center(15), "Name".center(15), "Phone".center(15), "ISBN".center(15))
    for customer in cur.fetchall():
        print(str(customer[0]).center(15), customer[1].center(15), str(customer[2]).center(15), str(customer[3]).center(15))
    print("".center(150, '-'))

def search_book():
    print()
    print('Search'.center(30,'-'))
    print('Search on the basis of : ')
    print('1. ISBN Number')
    print('2. Book Title')
    print('3. Author Name')
    print('4. Publisher Name')
    choice = int(input('Enter your choice : '))
    if choice == 1:
        search_value = int(input('Enter ISBN Number(5 Digits) : '))
        cur.execute(f'select * from books where isbn = {search_value}')
        lst = cur.fetchall()
        if len(lst) == 0:
            print('No Book with the ISBN Provided')
        else:
            print('Book Detail : ')
            for book in lst[0]:
                print(book, end='\t')
    elif choice == 2:
        search_value = input('Enter Book Title : ')
        cur.execute(f"select * from books where title = '{search_value}'")
        lst = cur.fetchall()
        if len(lst) == 0:
            print('No Book with the title Provided')
        else:
            print('Book Detail : ')
            for book in lst:
                print(book, end='\t')
    elif choice  == 3:
        search_value = input('Enter the Author Name : ')
        cur.execute(f"select * from books where author = '{search_value}'")
        lst = cur.fetchall()
        if len(lst) == 0:
            print('No Book with the author name Provided')
        else:
            print('Book Detail : ')
            for book in lst:
                print(book, end='\t')
    elif choice == 4:
        search_value = input('Enter the Publisher : ')
        cur.execute(f"select * from books where publisher = '{search_value}'")
        lst = cur.fetchall()
        if len(lst) == 0:
            print('No Book with the publisher name Provided')
        else:
            print('Book Detail : ')
            for book in lst:
                print(book, end='\t')
    else:
        print('Wrong Choice Given!!')
    
    print()
    
def delete_book():
    print()
    print("********** DELETE ************")
    isbn = int(input('Enter ISBN No. : '))

    query = f"select * from books where isbn ={isbn}"
    cur.execute(query)

    lst = cur.fetchall()
    if len(lst) != 0:
        try:
            cur.execute(f"delete from books where isbn = {isbn}")
            con.commit()
        except:
            print('Customer Exist with the book purchased')        
    else:
        print(f'No record with ISBN = {isbn}')

    print("******************************")
    print()



def view_books():
    print()
    query = "select * from books"
    cur.execute(query)
    lst = cur.fetchall()
    if len(lst) == 0:
        print('\n---No Books to display----\n')
        return

    print('Displaying Records'.center(150, '-'))
    print("ISBN".center(15), "Title".center(15), "Author".center(15), "Publisher".center(15), "Price".center(15), "Quantity Sold".center(15), "Total Sales".center(15))
    for book in lst:
        print(str(book[0]).center(15), book[1].center(15), book[2].center(15), book[3].center(15), str(book[4]).center(15), str(book[5]).center(15), str(book[6]).center(15))
    print("".center(150, '-'))
    print()

def update_book():
    print()
    print('****Update Records*****')
    isbn = int(input('Enter ISBN No. : '))
    query = f"select * from books where isbn = {isbn}"
    cur.execute(query)
    lst = cur.fetchall()

    if len(lst) != 0:
        price = int(input('Enter the new price : '))
        query = f"update books set price = {price} where isbn = {isbn}"
        cur.execute(query)
        con.commit()

        query1 = f"update books set total_sales = price * quantity_sold where isbn = {isbn}"
        cur.execute(query1)
        con.commit()
        print('Record Updated Successfully')
    else:
        print(f'No Book With the ISBN {isbn} provided')
    print('***********************')
    print()

def add_book():
    global total_sales
    total_sales = 0
    quantity_sold = 0 #because we want to initialize the value of quantity_sold to be 0 at the time of addition.
    print()
    print('Add Books'.center(30, '*'))
    print('Please Provide Book Details ----->')
    isbn = input('Enter ISBN No.(5 Digits) : ')
    if len(isbn) == 5 and isbn.isdigit():
        title = input('Enter Book Title : ')
        author = input('Enter Book Author : ')
        publisher = input('Enter Book Publisher : ')
        price = int(input('Enter the book price : '))
    

        # Writing Queries
        isbn = int(isbn)
        query = f"insert into books values({isbn}, '{title}', '{author}', '{publisher}', {price}, {quantity_sold}, {total_sales})"
        print(query)
        # Now Executing the query
        cur.execute(query)
        con.commit()
        print('***********Record Inserted Successfully*********')
    else:
        print('>>>>>>Please Provide ISBN Number Correctly <<<<<<<')
    print()

def start(userid):
    while True:
        print('MAIN MENU'.center(50,'-'))
        print('1. Add Book Details')
        print('2. Update Book Details')
        print('3. View All Books')
        print('4. Delete Book')
        print('5. Search Book')
        print('6. Add Customer Details')
        print('7. View All Customers')
        print('8. Exit')
        choice = int(input('Enter your choice : '))
        if choice == 1:
            add_book()
        elif choice == 2:
            update_book()
        elif choice == 3:
            view_books()
        elif choice == 4:
            delete_book()
        elif choice == 5:
            search_book()
        elif choice == 6:
            customer_purchase()
        elif choice == 7:
            view_customers()
        elif choice == 8:
            print(f'THANKYOU {userid}'.center(50,'-'))
            break
        else:
            print('Wrong choice given !!')
            print()


def main():
    print('---------------Enter Your Credentials to Login-----------------')
    userid = input('Enter your user id : ')
    password = input('Enter your password : ')
    #Executing Queries
    query = 'SELECT * FROM LOGIN_BOOK'
    cur.execute(query)
    for det in cur.fetchall():
        if userid == det[0]:
            if password == det[1]:
                start(userid)

            else:
                print(f'Wrong Password for {userid}')
            break
    else:
        print(f'Wrong userid, \nuserid {userid} doesn\'t exists')

main()

```

</details>

In this way the project involves the knowledge of both the Python and MySQL.
