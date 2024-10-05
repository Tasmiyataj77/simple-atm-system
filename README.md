# simple-atm-system
#include <iostream>
#include <string>

using namespace std;

class ATM {
private:
    string userPIN;
    double balance;

public:
    // Constructor to initialize account details
    ATM(string pin, double initialBalance) {
        userPIN = pin;
        balance = initialBalance;
    }

    // Function to authenticate user with PIN
    bool authenticate(string inputPIN) {
        return inputPIN == userPIN;
    }

    // Function to check the current balance
    void checkBalance() {
        cout << "\nYour current balance is: $" << balance << endl;
    }

    // Function to deposit money
    void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            cout << "\nYou've successfully deposited $" << amount << endl;
        } else {
            cout << "\nInvalid deposit amount!" << endl;
        }
    }

    // Function to withdraw money
    void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            cout << "\nYou've successfully withdrawn $" << amount << endl;
        } else if (amount > balance) {
            cout << "\nInsufficient balance!" << endl;
        } else {
            cout << "\nInvalid withdrawal amount!" << endl;
        }
    }
};

int main() {
    string pin = "1234";  // User PIN (preset for simplicity)
    double initialBalance = 1000.00;  // Initial balance for the account
    ATM atm(pin, initialBalance);

    string inputPIN;
    int choice;
    double amount;

    cout << "Welcome to the ATM!" << endl;

    // PIN Authentication
    cout << "\nPlease enter your PIN: ";
    cin >> inputPIN;

    if (atm.authenticate(inputPIN)) {
        cout << "\nAuthentication successful!\n";

        do {
            // Display options to the user
            cout << "\nATM Menu: " << endl;
            cout << "1. Check Balance" << endl;
            cout << "2. Deposit Money" << endl;
            cout << "3. Withdraw Money" << endl;
            cout << "4. Exit" << endl;
            cout << "Enter your choice: ";
            cin >> choice;

            switch (choice) {
            case 1:
                atm.checkBalance();
                break;
            case 2:
                cout << "\nEnter amount to deposit: $";
                cin >> amount;
                atm.deposit(amount);
                break;
            case 3:
                cout << "\nEnter amount to withdraw: $";
                cin >> amount;
                atm.withdraw(amount);
                break;
            case 4:
                cout << "\nThank you for using the ATM. Goodbye!" << endl;
                break;
            default:
                cout << "\nInvalid choice! Please try again." << endl;
            }
        } while (choice != 4);

    } else {
        cout << "\nAuthentication failed! Incorrect PIN." << endl;
    }

    return 0;
}
