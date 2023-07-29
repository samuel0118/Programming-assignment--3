# Programming-assignment--3// Copyright 2023
// Author: Samuel Olabode Onifade

#include <iostream>
#include <fstream>
#include <string>

// Using-declarations to bring in specific items from the std namespace
using std::cout;
using std::cin;
using std::endl;
using std::string;
using std::ifstream;
using std::ofstream;

// Function prototypes
void printMenu();
void login();
void registration();
void forgot();

int main() {
    int choice;

    cout << "Welcome to my Application  " << endl;

    /* Loop to display the menu and 
    handle user input until the user 
    chooses to exit*/
    while (true) {
        printMenu();
        cin >> choice;
        cout << endl;

        switch (choice) {
        case 1:
            login();
            break;
        case 2:
            registration();
            break;
        case 3:
            forgot();
            break;
        case 4:
            cout << "Thank you!" << endl;
            return 0;  // Exit the program
        default:
            cout << "Invalid choice. Please select "\
            "from the options given above" << endl;
            break;
        }
    }

    return 0;
}

void printMenu() {
    cout << "Please enter your selection: " << endl;
    cout << "1. Login" << endl;
    cout << "2. Register" << endl;
    cout << "3. Forgot password " << endl;
    cout << "4. Exit" << endl;
}

void login() {
    int count = 0;
    string username, password, storedUsername, storedPassword;
    cout << "Enter your username: ";
    cin >> username;
    cout << "Enter your password: ";
    cin >> password;

    ifstream input("users.txt");

    // Check if the file is open and readable
    if (!input) {
        cout << "Error opening file. Please try again later." << endl;
        return;
    }

    while (input >> storedUsername >> storedPassword) {
        if (username == storedUsername && password == storedPassword) {
            count = 1;
            break;
        }
    }
    input.close();

    if (count == 1) {
        cout << storedUsername << " Your login is successful." << endl;
        cout << "You now have access to services  3, and 4." << endl;
    } else {
        cout << "Login error: Invalid username and password." << endl;
    }
}

void registration() {
    string rusername, rpassword;
    cout << "Enter the username: ";
    cin >> rusername;
    cout << "Enter the password: ";
    cin >> rpassword;
    cout << endl;

    ofstream f1("users.txt", std::ios_base::app);

    // Check if the file is open and writable
    if (!f1) {
        cout << "Error opening file. Please try again later." << endl;
        return;
    }

    f1 << rusername << ' ' << rpassword << endl;
    f1.close();
    cout << "Registration is successful." << endl;
}

void forgot() {
    int option;
    cout << "Forgot your password?" << endl;
    cout << "Press 1 to reset password" << endl;
    cout << "Press 2 to go back to the main menu" << endl;
    cout << "Enter your choice: ";
    cin >> option;

    switch (option) {
    case 1: {
        int count = 0;
        string susername, storedUsername, storedPassword;
        cout << "Enter your username: ";
        cin >> susername;

        ifstream f2("users.txt");

        // Check if the file is open and readable
        if (!f2) {
            cout << "Error opening file. Please try again later." << endl;
            return;
        }

        while (f2 >> storedUsername >> storedPassword) {
            if (susername == storedUsername) {
                count = 1;
                break;
            }
        }
        f2.close();

        if (count == 1) {
            cout << "Your account is found." << endl;
            cout << "Your password is: " << storedPassword << endl;
        } else {
            cout << "Sorry! Your account is not found!" << endl;
        }
        break;
    }
    case 2:
        break;  // Do nothing, just return to the main menu
    default:
        cout << "Wrong choice! Please try again." << endl;
        break;
    }
}
