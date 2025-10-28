# Employee Management System

**An Employee Management System is a software application used by organizations to manage their employee data. It helps to keep track of employee information such as their personal details, job position, salary, and other related data. It is designed to streamline HR operations and automate administrative tasks related to employees.**\
\
**You** have to build a basic employee management system using python which should perform the following functions -

1. **Add Employee**\
   In this, employee details can be added. The details will include the **ID,** **Name, Age, Gender, Job Position** and **salary**. Also a check will be applied to ensure uniqueness of the **Employee ID.**
2. **Update Employee**\
   In this, employee detail can be updated using **employee id**\
   Also a submenu will be provided to the user to choose for which information he wants to update. such as Name, Gender, etc. _**ID for the employee will not be updated once defined it will remain same for the concerned employee.**_
3. **Delete Employee**\
   In this, An employee can be deleted using the **employee ID.**
4. **List Employee**\
   In this, List of all the employees will be shown to the user in tabular format.
5. **Exit**\
   **Now at the end your program will ask the user to exit from the program.** \\

**These options will be provided to the user each and every time the user performs an operation successfully such as addition or deletion of the employee.**\
This program doesn't to be a **GUI** application, it will be simple console based and will not involve the use of database and database applications such as MY SQL, SQL Server, etc.\
\
Here are some Examples:

{% tabs %}
{% tab title="User View" %}
**----Employee Management System-----**

1. **Add Employee**
2. **Update Employee**
3. **Delete Employee**
4. **List Employees**
5. **Exit**

**Enter your choice:** 1
{% endtab %}

{% tab title="Add Employee" %}
**Enter Employee Details:**

**ID**: 101\
**Name:** Mohan\
**Age:** 20\
**Gender:** Male\
**Position:** Manager\
**Salary:** 100000\
**Employee added successfully.**
{% endtab %}

{% tab title="Update Details" %}
\*\*Enter the Employee ID\*\*

**ID: 101**\
Which Information you want to update :

1. Name
2. Age
3. Gender
4. Position
5. Salary\
   **Enter Your choice :** 3\
   **Gender : Male**\
   **Enter the Gender :** Female\
   **Employee Details updated Successfully**
{% endtab %}

{% tab title="Delete Employee" %}
Enter Employee ID:\
ID: 101\
Employee deleted successfully.
{% endtab %}

{% tab title="Display" %}
<table><thead><tr><th width="88">ID</th><th width="106">Name</th><th>Age</th><th>Gender</th><th>Position</th><th>Salary</th></tr></thead><tbody><tr><td>101</td><td>Mohan</td><td>20</td><td>Male</td><td>Manager</td><td>100000</td></tr><tr><td>102</td><td>Madan</td><td>20</td><td>Male</td><td>Asst. Manager</td><td>80000</td></tr><tr><td>103</td><td>Damodar</td><td>22</td><td>Male</td><td>Clerk</td><td>20000</td></tr></tbody></table>
{% endtab %}

{% tab title="Exit" %}
Program Exited!!
{% endtab %}
{% endtabs %}

You can further Improve your project on your own by adding some more functionalities and features.

<details>

<summary>Solution</summary>

```python
# Employee Management System

#Globally a list has been created for employees to add
employees = []

# Add Employee
def add_employee():
    flag = True # for checking the uniqueness of the ID of the employee
    print("Enter Employee Details:")
    id = int(input("ID: "))
    name = input("Name: ")
    age = int(input("Age: "))
    gender = input("Gender: ")
    position = input("Position: ")
    salary = float(input("Salary: "))
    #Now Checking whether the ID provided by the user already exists or not
    if not employees:
        flag = True
    else:
        for emp in employees:
            if id  == emp['id']:
                flag = False
                break
    if flag == True:
        #If ID is unique then add the details

        #Dictionary of employee with his details as key value pair has been added
        employee = {'id': id, 'name': name, 'age': age, 'gender': gender, 'position': position, 'salary': salary}

        #Now this detail is added in that globally declared list.
        employees.append(employee)
        print("Employee added successfully.")
    else:
        print('ID already exists!!')

# Update Employee
def update_employee():
    #Taking ID from the user on which update is to be performed.
    print("Enter Employee ID:")
    id = int(input("ID: "))
    
    #Loop for finding the employee with the ID provided to update details
    for employee in employees:
        if employee['id'] == id: #condition for finding the employee
            print('Which Information you want to update : ')
            print('1. Name')
            print('2. Age')
            print('3. Gender')
            print('4. Position')
            print('5. Salary')
            ch = int(input('Enter Your choice : '))

            #Now checking for which information has to be updated
            #On deciding, first line will show the current value of that column
            #Second, new value will be asked from the user to update
            if ch == 1:
                #showing the current value of column name
                print('Name : ', employee['name'])
                #Taking the new value from the user to update
                employee['name'] = input('Enter the new name :')
            elif ch == 2:
                print('Age : ', employee['age'])
                employee['age'] = input('Enter the age :')
            elif ch == 3:
                print('Gender :', employee['gender'])
                employee['gender'] = input('Enter the Gender : ')
            elif ch == 4:
                print('Name : ', employee['position'])
                employee['position'] = input('Enter the position :')
            elif ch == 5:
                print('Salary : ', employee['salary'])
                employee['salary'] = input('Enter the salary :')
            print('Employee Details updated Successfully')
            print()
            #On successfully adding the employee
            #return statement will return the control the while loop of options from
            #add function to the while loop
            return
    #If employee with the ID provided is not found then no return
    #statement will be executed and thus employee not found message
    #Will be displayed to the user as written below.
    print("Employee not found.")

# Delete Employee
def delete_employee():
    print("Enter Employee ID:")
    id = int(input("ID: "))
    for employee in employees:
        if employee['id'] == id:
            #On finding the employee with the concerned details
            #Employee is removed from list employees using remove function of list
            employees.remove(employee)
            print("Employee deleted successfully.")
            return
        #here same logic for return is applied as explained in above add function.
    print("Employee not found.")

# List Employees
def list_employees():
    if len(employees) == 0:
        print("No employees found.")
        return
    #Printing in tabular format
    print("ID\tName\tAge\tGender\tPosition\tSalary")
    print()
    for employee in employees:
        print(f"{employee['id']}\t{employee['name']}\t{employee['age']}\t{employee['gender']}\
\t{employee['position']}\t{employee['salary']}")
# Main Loop
while True:
    #Through this loop the execution of the program starts
    #and this is the user view
    print()
    print("----Employee Management System-----")
    print("1. Add Employee")
    print("2. Update Employee")
    print("3. Delete Employee")
    print("4. List Employees")
    print("5. Exit")
    choice = int(input("Enter your choice: "))
    if choice == 1:
        add_employee()
    elif choice == 2:
        update_employee()
    elif choice == 3:
        delete_employee()
    elif choice == 4:
        list_employees()
    elif choice == 5:
        print('Program Exited!!')
        break
    else:
        print("Invalid choice. Please try again.")

```

</details>

<details>

<summary>Code Explanation</summary>

The above code starts from the while loop and that is the user view means first time the user interacts with the options provided there.

On choosing the options user is asked for the necessary details to be added.

A list `employees = []` has been declared globally to add employees with their details in the form of **dictionary**. It is declared globally so that it is available throughout the program.

`add_employee()` function is defined to add the employee which takes the employee id from the user and checks whether any user with the ID provided exists or not. If yes then a message is displayed that user already exist otherwise the details are added in the form of **dictionary in the list employees\[] declared globally**

`update_employee()` function updates the employee details by taking the user id and finds the employee with that employee id and displays a submenu to the user asking which detail user want to update. Each option shows its old value and asks for the new value from the user.

`delete_employee()` function deleted the employee on the basis of employee ID.

`list_employees()`function displays list of all the employees in the tabular format.

Inside these functions on few places **return** is used to return the control to the while loop if the employee is found and the necessary operation is performed successfully. If the employee is not found then this **return** statement will not be executed as the control will not come inside the if block then **a message&#x20;**_**Employee not found**_**&#x20;is displayed to the user.**

</details>
