# INTERNEPEDIA-task-2
# tast 2, To-Do List

# To-Do List Application
# Initialize an empty list to store tasks
tasks = []
# Load tasks from file if it exists
try:
    with open("tasks.txt", "r") as file:
        tasks = [line.strip().split(",") for line in file.readlines()]
except FileNotFoundError:
    pass

def display_tasks():
    print("\nTo-Do List:")
    for i, task in enumerate(tasks, start=1):
        status = "Done" if task[1] == "1" else "Undone"
        print(f"{i}. {task[0]} - {status}")

def add_task():
    task_name = input("Enter task name: ")
    tasks.append([task_name, "0"])
    print("Task added!")

def mark_task():
    display_tasks()
    task_number = int(input("Enter task number to mark as done/undone: ")) - 1
    if task_number >= 0 and task_number < len(tasks):
        tasks[task_number][1] = "1" if tasks[task_number][1] == "0" else "0"
        print("Task marked!")
    else:
        print("Invalid task number.")

def remove_task():
    display_tasks()
    task_number = int(input("Enter task number to remove: ")) - 1
    if task_number >= 0 and task_number < len(tasks):
        tasks.pop(task_number)
        print("Task removed!")
    else:
        print("Invalid task number.")

def save_tasks():
    with open("tasks.txt", "w") as file:
        for task in tasks:
            file.write(",".join(task) + "\n")
    print("Tasks saved!")

while True:
    print("\nTo-Do List Menu:")
    print("1. Display Tasks")
    print("2. Add Task")
    print("3. Mark Task")
    print("4. Remove Task")
    print("5. Save Tasks")
    print("6. Exit")

    choice = input("Enter your choice (1-6): ")

    if choice == "6":
        print("Goodbye!")
        break
    elif choice in ["1", "2", "3", "4", "5"]:
        {
            "1": display_tasks,
            "2": add_task,
            "3": mark_task,
            "4": remove_task,
            "5": save_tasks
        }[choice]()
    else:
        print("Invalid choice. Please choose a valid option.")
