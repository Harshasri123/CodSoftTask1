import os

class ToDoList:
    def _init_(self, filename="todolist.txt"):
        self.filename = filename
        self.tasks = self.load_tasks()

    def load_tasks(self):
        tasks = []
        if os.path.exists(self.filename):
            with open(self.filename, "r") as file:
                tasks = [line.strip() for line in file.readlines()]
        return tasks

    def save_tasks(self):
        with open(self.filename, "w") as file:
            for task in self.tasks:
                file.write(task + "\n")

    def display_tasks(self):
        if not self.tasks:
            print("No tasks found.")
        else:
            print("Tasks:")
            for index, task in enumerate(self.tasks, start=1):
                print(f"{index}. {task}")

    def add_task(self, task):
        self.tasks.append(task)
        self.save_tasks()
        print(f"Task '{task}' added successfully.")

    def complete_task(self, task_index):
        if 1 <= task_index <= len(self.tasks):
            completed_task = self.tasks.pop(task_index - 1)
            self.save_tasks()
            print(f"Task '{completed_task}' marked as completed.")
        else:
            print("Invalid task index.")

def main():
    todo_list = ToDoList()

    while True:
        print("\nTODO LIST APPLICATION")
        print("1. Display Tasks")
        print("2. Add Task")
        print("3. Complete Task")
        print("4. Exit")

        choice = input("Enter your choice (1-4): ")

        if choice == "1":
            todo_list.display_tasks()
        elif choice == "2":
            task = input("Enter the task: ")
            todo_list.add_task(task)
        elif choice == "3":
            task_index = int(input("Enter the task index to mark as completed: "))
            todo_list.complete_task(task_index)
        elif choice == "4":
            print("Exiting the application. Goodbye!")
            break
        else:
            print("Invalid choice. Please enter a number between 1 and 4.")

if _name_ == "_main_":
    main()
