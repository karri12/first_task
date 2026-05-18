# Task Management App with Recommendations
# Features:
# 1. Add Task
# 2. Remove Task
# 3. List Tasks
# 4. Prioritize Tasks
# 5. Task Recommendations based on descriptions

class Task:
    def __init__(self, name, description, priority="Medium"):
        self.name = name
        self.description = description
        self.priority = priority

    def __str__(self):
        return f"Task: {self.name} | Priority: {self.priority}\nDescription: {self.description}"


class TaskManager:
    def __init__(self):
        self.tasks = []

    # Add Task
    def add_task(self):
        name = input("Enter task name: ")
        description = input("Enter task description: ")
        priority = input("Enter priority (High/Medium/Low): ")

        task = Task(name, description, priority)
        self.tasks.append(task)

        print("Task added successfully!\n")

    # Remove Task
    def remove_task(self):
        name = input("Enter task name to remove: ")

        for task in self.tasks:
            if task.name.lower() == name.lower():
                self.tasks.remove(task)
                print("Task removed successfully!\n")
                return

        print("Task not found!\n")

    # List Tasks
    def list_tasks(self):
        if not self.tasks:
            print("No tasks available.\n")
            return

        print("\n----- Task List -----")
        for i, task in enumerate(self.tasks, start=1):
            print(f"{i}. {task}")
        print()

    # Sort by Priority
    def prioritize_tasks(self):
        priority_order = {
            "High": 1,
            "Medium": 2,
            "Low": 3
        }

        self.tasks.sort(
            key=lambda task: priority_order.get(task.priority, 2)
        )

        print("Tasks prioritized successfully!\n")

    # Recommendation System
    def recommend_task_type(self):
        description = input("Enter task description for recommendation: ")

        keywords = {
            "study": "Recommended Priority: High",
            "exam": "Recommended Priority: High",
            "project": "Recommended Priority: High",
            "meeting": "Recommended Priority: Medium",
            "exercise": "Recommended Priority: Medium",
            "shopping": "Recommended Priority: Low",
            "movie": "Recommended Priority: Low"
        }

        found = False

        for word, recommendation in keywords.items():
            if word in description.lower():
                print(recommendation)
                found = True
                break

        if not found:
            print("Recommended Priority: Medium")

        print()

    # Menu
    def run(self):
        while True:
            print("===== TASK MANAGEMENT APP =====")
            print("1. Add Task")
            print("2. Remove Task")
            print("3. List Tasks")
            print("4. Prioritize Tasks")
            print("5. Get Task Recommendation")
            print("6. Exit")

            choice = input("Enter your choice: ")

            if choice == "1":
                self.add_task()

            elif choice == "2":
                self.remove_task()

            elif choice == "3":
                self.list_tasks()

            elif choice == "4":
                self.prioritize_tasks()

            elif choice == "5":
                self.recommend_task_type()

            elif choice == "6":
                print("Exiting application...")
                break

            else:
                print("Invalid choice! Try again.\n")


# Main Program
task_manager = TaskManager()
task_manager.run()
