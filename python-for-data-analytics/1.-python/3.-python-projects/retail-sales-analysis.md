# Retail Sales Analysis

### Scenario

**You work for a small cafe that sells various types of coffee, tea, and pastries. The owner has asked you to create a program that helps them keep track of their inventory and sales. The owner wants to be able to add new items to the menu, update the quantities of existing items, and see a summary of the total sales for each item at the end of the day.**

### Instructions

Write a Python program that allows the **cafe** owner to perform the following actions:

1. **Add new items to the menu:** The program should ask the user to enter the name, category, price, and quantity of a new item. The program should then add the item to a menu list.
2. **Update the quantities of existing items:** The program should display a table of all the items in the menu list with their corresponding quantities. The user should be prompted to enter the name of the item they want to update and the new quantity. The program should then update the quantity of the specified item.
3. **View the summary of total sales for each item:** The program should display a table of all the items in the menu list with their corresponding quantities and total sales. The total sales should be calculated as the product of the price and quantity of each item sold during the day.
4. **Sales Analysis at the end price wise :** At the end, through program one should be able to see the sales price in descending order means item with highest sale should be the first item to be seen in the list.

{% tabs %}
{% tab title="User View" %}
**Welcome to the cafe inventory and sales tracker!**

**What would you like to do?**

1. **Add new item to menu**
2. **Update item quantities**
3. **View sales summary**
4. **Quit**

**Enter your choice (1-4):** 1
{% endtab %}

{% tab title="Add Item" %}
**Welcome to the cafe inventory and sales tracker!**

**What would you like to do?**

1. **Add new item to menu**
2. **Update item quantities**
3. **View sales summary**
4. **Quit**

**Enter your choice (1-4):** 1

**Enter the name of the item:** Coffee\
**Enter the category of the item:** Beverages\
**Enter the price of the item:** 2.50\
**Enter the quantity of the item:** 10

Item added to menu:\
Name: Coffee\
Category: Beverages\
Price: $2.50\
Quantity: 10
{% endtab %}

{% tab title="Update Item" %}
**Enter the name of the item you want to update:** Coffee\
**Enter the new quantity:** 5

**Item quantity updated:**

**Name:** Coffee

**New quantity:** 5
{% endtab %}

{% tab title="View Items" %}
<table><thead><tr><th width="168.66666666666666">Name</th><th>Category</th><th>Price</th><th>Quantity</th><th>Total Sales</th></tr></thead><tbody><tr><td>Coffee</td><td>Beverages</td><td>2.50</td><td>10</td><td>25</td></tr><tr><td>Pizza</td><td>Main Dishes</td><td>10.99</td><td>15</td><td>164.85</td></tr><tr><td>Salad</td><td>Appetizers</td><td>5.99</td><td>8</td><td>47.92</td></tr></tbody></table>
{% endtab %}

{% tab title="Sales Analysis" %}
**Item Sales :**\
Pizza : 164.85\
Salad : 47.92\
Coffee : 25.0
{% endtab %}
{% endtabs %}

<details>

<summary>Solution</summary>

```python
# Define menu list
menu = []

# Define function to add new item to menu
def add_item():
    # Prompt user for item details
    name = input("Enter the name of the item: ")
    category = input("Enter the category of the item: ")
    price = float(input("Enter the price of the item: "))
    quantity = int(input("Enter the quantity of the item: "))
    
    # Add item to menu list
    menu.append({
        "name": name,
        "category": category,
        "price": price,
        "quantity": quantity
    })
    
    # Print confirmation message
    print("Item added to menu:")
    print("Name:", name)
    print("Category:", category)
    print("Price: ${:.2f}".format(price))
    print("Quantity:", quantity)

# Define function to update item quantities
def update_quantity():
    # Print current menu
    print("Current menu:")
    print("Name\tCategory\tPrice\tQuantity")
    for item in menu:
        print(f"{item['name']}\t{item['category']}\t${item['price']}\t{item['quantity']}")
    
    # Prompt user for item to update and new quantity
    name = input("Enter the name of the item you want to update: ")
    quantity = int(input("Enter the new quantity: "))
    
    # Update quantity of specified item
    for item in menu:
        if item["name"] == name:
            item["quantity"] = quantity
            # Print confirmation message
            print("Item quantity updated:")
            print("Name:", name)
            print("New quantity:", quantity)
            return
    
    # Print error message if item not found
    print("Error: Item not found in menu")

# Define function to view sales summary
def view_summary():
    # Print sales summary
    print("Sales summary:")
    print("Name\tCategory\tPrice\tQuantity\tTotal sales")
    for item in menu:
        total_sales = item["price"] * item["quantity"]
        print(f"{item['name']}\t{item['category']}\t${item['price']}\t{item['quantity']}\t${total_sales}")

#To get the sales total sales wise from top to bottom
def get_top():
    sales = []
    for item in menu:
        sales.append((item['name'], item["price"]*item["quantity"]))
    print('Item Sales : ')
    sales.sort(key = lambda a:a[-1], reverse = True)
    for name, value in sales:
        print(f'{name} : {value}')

# Main program loop
while True:
    # Print menu
    print()
    print("\nWelcome to the cafe inventory and sales tracker!\n")
    print("What would you like to do?")
    print("1. Add new item to menu")
    print("2. Update item quantities")
    print("3. View sales summary")
    print("4. View Sales Analysis")
    print("5. Quit")
    
    # Prompt user for choice
    choice = input("\nEnter your choice (1-4): ")
    
    # Perform action based on user choice
    if choice == "1":
        add_item()
    elif choice == "2":
        update_quantity()
    elif choice == "3":
        view_summary()
    elif choice == "4":
        get_top()
    elif choice == "5":
        print("\nGoodbye!")
        break
    else:
        print("Error: Invalid choice")

```

</details>
