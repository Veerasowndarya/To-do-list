#include <iostream>
#include <vector>
#include <string>

using namespace std;

struct Task {
    string description;
    bool completed;

    Task(string desc) : description(desc), completed(false) {}
};

class ToDoListManager {
private:
    vector<Task> tasks;

public:
    void addTask(const string& task) {
        tasks.emplace_back(task);
        cout << "Task '" << task << "' added." << endl << endl;
    }

    void viewTasks() {
        if (tasks.empty()) {
            cout << "No tasks in the list." << endl << endl;
            return;
        }
        for (size_t i = 0; i < tasks.size(); ++i) {
            cout << i + 1 << ". " << tasks[i].description
                 << " - " << (tasks[i].completed ? "Completed" : "Pending") << endl;
        }
        cout << endl;
    }

    void markTaskCompleted(size_t taskIndex) {
        if (taskIndex >= 1 && taskIndex <= tasks.size()) {
            tasks[taskIndex - 1].completed = true;
            cout << "Task '" << tasks[taskIndex - 1].description << "' marked as completed." << endl << endl;
        } else {
            cout << "Invalid task number." << endl << endl;
        }
    }

    void removeTask(size_t taskIndex) {
        if (taskIndex >= 1 && taskIndex <= tasks.size()) {
            cout << "Task '" << tasks[taskIndex - 1].description << "' removed." << endl << endl;
            tasks.erase(tasks.begin() + taskIndex - 1);
        } else {
            cout << "Invalid task number." << endl << endl;
        }
    }
};

int main() {
    ToDoListManager manager;
    int choice;
    string task;
    size_t taskIndex;

    while (true) {
        cout << "To-Do List Manager" << endl;
        cout << "1. Add Task" << endl;
        cout << "2. View Tasks" << endl;
        cout << "3. Mark Task as Completed" << endl;
        cout << "4. Remove Task" << endl;
        cout << "5. Exit" << endl;
        cout << "Choose an option: ";
        cin >> choice;
        cin.ignore(); // To ignore the newline character left in the buffer

        switch (choice) {
        case 1:
            cout << "Enter the task: ";
            getline(cin, task);
            manager.addTask(task);
            break;
        case 2:
            manager.viewTasks();
            break;
        case 3:
            cout << "Enter the task number to mark as completed: ";
            cin >> taskIndex;
            manager.markTaskCompleted(taskIndex);
            break;
        case 4:
            cout << "Enter the task number to remove: ";
            cin >> taskIndex;
            manager.removeTask(taskIndex);
            break;
        case 5:
            cout << "Exiting To-Do List Manager. Goodbye!" << endl;
            return 0;
        default:
            cout << "Invalid choice. Please choose a valid option." << endl << endl;
        }
    }
}
