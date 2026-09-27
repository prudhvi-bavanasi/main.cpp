# main.cpp
Student Management System (C++)

#include <iostream>
#include <fstream>
#include <string>

using namespace std;

class Student {
private:
    string name;
    int rollNo;
    string course;

public:
    void addStudent() {
        cout << "Enter Name: ";
        cin.ignore();
        getline(cin, name);
        cout << "Enter Roll Number: ";
        cin >> rollNo;
        cout << "Enter Course: ";
        cin.ignore();
        getline(cin, course);

        ofstream outFile("students.txt", ios::app);
        if (outFile.is_open()) {
            outFile << rollNo << "," << name << "," << course << "\n";
            cout << "Student Record Added Successfully!\n";
            outFile.close();
        } else {
            cout << "Error opening file!\n";
        }
    }

    void viewStudents() {
        ifstream inFile("students.txt");
        string line;
        cout << "\n--- Student Records ---\n";
        if (inFile.is_open()) {
            while (getline(inFile, line)) {
                cout << line << "\n";
            }
            inFile.close();
        } else {
            cout << "No records found.\n";
        }
        cout << "-----------------------\n";
    }
};

int main() {
    Student s;
    int choice;

    do {
        cout << "\n1. Add Student\n2. View Students\n3. Exit\nEnter Choice: ";
        cin >> choice;

        switch (choice) {
            case 1: s.addStudent(); break;
            case 2: s.viewStudents(); break;
            case 3: cout << "Exiting...\n"; break;
            default: cout << "Invalid Choice\n";
        }
    } while (choice != 3);

    return 0;
}
