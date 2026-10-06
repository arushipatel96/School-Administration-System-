# School-Administration-System-
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

class Student
{
public:
    int id;
    string name;
    int age;

    void addStudent()
    {
        ofstream file("students.txt", ios::app);
        cout << "Enter ID: ";
        cin >> id;
        cin.ignore();
        cout << "Enter Name: ";
        getline(cin, name);
        cout << "Enter Age: ";
        cin >> age;

        file << id << " " << name << " " << age << endl;
        file.close();

        cout << "\nStudent Added Successfully.\n";
    }

    void viewStudents()
    {
        ifstream file("students.txt");
        string line;

        cout << "\n----- Student Records -----\n";

        while (getline(file, line))
            cout << line << endl;

        file.close();
    }

    void searchStudent()
    {
        ifstream file("students.txt");
        int sid;
        string sname;
        int sage;
        int searchId;
        bool found = false;

        cout << "Enter Student ID: ";
        cin >> searchId;

        while (file >> sid >> sname >> sage)
        {
            if (sid == searchId)
            {
                cout << "\nID: " << sid;
                cout << "\nName: " << sname;
                cout << "\nAge: " << sage << endl;
                found = true;
            }
        }

        if (!found)
            cout << "\nStudent Not Found.\n";

        file.close();
    }
};

int main()
{
    string user, pass;

    cout << "===== SCHOOL ADMINISTRATION MANAGEMENT SYSTEM =====\n\n";

    cout << "Username: ";
    cin >> user;

    cout << "Password: ";
    cin >> pass;

    if (user != "admin" || pass != "1234")
    {
        cout << "\nInvalid Login.";
        return 0;
    }

    Student s;
    int choice;

    do
    {
        cout << "\n\n===== MAIN MENU =====\n";
        cout << "1. Add Student\n";
        cout << "2. View Students\n";
        cout << "3. Search Student\n";
        cout << "4. Exit\n";
        cout << "Enter Choice: ";
        cin >> choice;

        switch (choice)
        {
        case 1:
            s.addStudent();
            break;

        case 2:
            s.viewStudents();
            break;

        case 3:
            s.searchStudent();
            break;

        case 4:
            cout << "\nThank You.";
            break;

        default:
            cout << "\nInvalid Choice.";
        }

    } while (choice != 4);

    return 0;
}
