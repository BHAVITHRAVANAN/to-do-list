# to-do-list
#include <iostream>
#include <string>
#include <vector>

using namespace std;

class Task {
private:
    string name;
    string description;
    string dueDate;
    bool completed;

public:
    Task(const string& name, const string& description, const string& dueDate)
        : name(name), description(description), dueDate(dueDate), completed(false) {}

    // Getters and setters for task properties
    string getName() const {
        return name;
    }

    void markCompleted() {
        completed = true;
    }

    void displayTask() const {
        cout << name << " (" << (completed ? "Completed" : "Pending") << ")\n";
        cout << "Description: " << description << "\n";
        cout << "Due Date: " << dueDate << "\n";
    }
};

class ToDoList {
private:
    vector<Task> tasks;

public:
    void addTask(const Task& task) {
        tasks.push_back(task);
    }

    void viewTasks() const {
        if (tasks.empty()) {
            cout << "No tasks found.\n";
        } else {
            cout << "Tasks:\n";
            for (const Task& task : tasks) {
                task.displayTask();
                cout << "\n";
            }
        }
    }

    void markTaskCompleted(const string& taskName) {
        for (Task& task : tasks) {
            if (task.getName() == taskName) {
                task.markCompleted();
                cout << "Task marked as completed.\n";
                return;
            }
        }
        cout << "Task not found.\n";
    }

    void deleteTask(const string& taskName) {
        for (auto it = tasks.begin(); it != tasks.end(); ++it) {
            if (it->getName() == taskName) {
                tasks.erase(it);
                cout << "Task removed.\n";
                return;
            }
        }
        cout << "Task not found.\n";
    }
};

int main() {
    ToDoList myToDoList;

    // Example usage:
    Task task1("Buy groceries", "Milk, eggs, bread", "2024-06-30");
    myToDoList.addTask(task1);

    // Display tasks
    myToDoList.viewTasks();

    // Mark a task as completed
    myToDoList.markTaskCompleted("Buy groceries");

    // Delete a task
    myToDoList.deleteTask("Buy groceries");

    return 0;
}
