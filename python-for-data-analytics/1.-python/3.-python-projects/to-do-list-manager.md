# To-Do List Manager

## To-Do List Manager

Let's go through each function in the code and explain their purpose:

1. `Create a variable tasks of list data type that contains no item.`

```
tasks=[]
```

2. ### Function to add a task

add\_task() :This function is responsible for adding a task to the `tasks` list. It prompts the user to enter a new task using the `input()` function. The entered task is then appended to the `tasks` list using the `append()` method. Finally, it prints a message to confirm that the task has been added successfully.

```
def add_task():
    task = input("Enter a new task: ")
    tasks.append(task)
    print("Task added successfully!")
```

### 3.Function to view tasks

`view_tasks()`: This function displays all the tasks in the `tasks` list. It first checks if the list is empty using a conditional statement. If the list is not empty, it iterates over the tasks using the `enumerate()` function. The `enumerate()` function provides both the index and the value of each task in the list. It then prints each task along with its corresponding index number. If the list is empty, it prints a message indicating that the task list is empty.

```
def view_tasks():
    if tasks:
        print("Your tasks:")
        for i, task in enumerate(tasks, start=1):
            print(f"{i}. {task}")
    else:
        print("Your task list is empty.")

```

### 4. Function to delete task

`delete_task()`: This function allows the user to delete a task from the `tasks` list. First, it calls the `view_tasks()` function to display the current tasks. It then prompts the user to enter the number of the task they want to delete. The input is converted to an integer and subtracted by 1 to align with the zero-based indexing of the list. Next, it checks if the entered task index is valid by comparing it with the range of valid indices in the list. If the index is valid, it uses the `pop()` method to remove the task at the specified index from the `tasks` list. It also prints a message to confirm the deletion of the task. If the entered index is invalid, it prints an error message.

```
def delete_task():
    view_tasks()
    task_index = int(input("Enter the task number to delete: ")) - 1
    if 0 <= task_index < len(tasks):
        deleted_task = tasks.pop(task_index)
        print(f"Deleted task: {deleted_task}")
    else:
        print("Invalid task number!")
```

### Creating a menu and calling the functions as per user's choice

Here, we are going to create a menu for the user to select the kind of task he wants to do.

```
while True:
        print("\n-- To-Do List Manager --")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Delete Task")
        print("4. Exit")

        choice = input("Enter your choice (1-4): ")

        if choice == "1":
            add_task()
        elif choice == "2":
            view_tasks()
        elif choice == "3":
            delete_task()
        elif choice == "4":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")
```
