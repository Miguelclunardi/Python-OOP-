# 🏦 Banking System with Python and OOP 🐍

Welcome to the Banking System project! This repository contains an implementation of a simple banking system, designed to clearly and practically demonstrate the fundamental pillars of Object-Oriented Programming (OOP): Encapsulation, Inheritance, and Polymorphism.

> **Note:** This is a provisional README for the initial phase of the project.

---

### 🎯 1. Project Objective

The main goal is to create a functional system that allows managing customers and different types of bank accounts (checking and savings). This project serves as a portfolio piece to demonstrate skills in software design, code organization, and the practical application of OOP concepts in Python.

### 📂 2. Folder and File Structure

Project organization is crucial for keeping the code modular, readable, and scalable. The adopted structure is as follows:

banking_system_oop/
├── src/
│   ├── init.py      # Makes 'src' a Python package
│   ├── account.py       # Contains the BankAccount, CheckingAccount, SavingsAccount classes
│   ├── customer.py      # Contains the Customer class
│   └── bank.py          # Contains the Bank class
├── main.py              # Program entry point (user interaction)
└── README.md            # Project documentation

### ⚙️ 3. Class Implementation

Below is a detailed description of each class and its requirements.

#### 📄 BankAccount Class (`src/account.py`)

This is the base class (superclass) that defines the common behavior and attributes for all accounts in the system.

-   **Attributes (private/protected):**
    -   `_account_number`: `str` or `int` (Unique identifier for the account).
    -   `_holder_name`: `str` (Name of the account holder).
    -   `_balance`: `float` (Current balance of the account, initialized to 0.0).

-   **Methods:**
    -   `__init__(self, account_number, holder_name, initial_balance=0.0)`: Class constructor.
    -   `deposit(self, amount)`: Adds an amount to the balance, if it is positive.
    -   `withdraw(self, amount)`: Standard withdrawal logic. This method will be overridden (polymorphism) in the child classes.
    -   `display_balance(self)`: Shows the account details and the current balance.
    -   `get_account_number(self)`, `get_holder_name(self)`, `get_balance(self)`: Getters for safe access to attributes.
    -   `__str__(self)`: Returns a formatted string representation of the object.

#### 💳 CheckingAccount Class (`src/account.py`)

Inherits from `BankAccount` and adds overdraft functionality.

-   **Inheritance:** Inherits from `BankAccount`.
-   **Additional Attributes:**
    -   `_overdraft_limit`: `float` (Maximum amount the balance can go negative).
-   **Methods:**
    -   `__init__(...)`: Calls the parent class constructor (`super().__init__()`) and initializes the limit.
    -   `withdraw(self, amount)`: (Polymorphism) Overrides the `withdraw` method, allowing withdrawals to use the balance plus the overdraft limit.

#### 💰 SavingsAccount Class (`src/account.py`)

Inherits from `BankAccount` and adds the functionality of interest yield.

-   **Inheritance:** Inherits from `BankAccount`.
-   **Additional Attributes:**
    -   `_interest_rate`: `float` (Percentage of interest to be applied).
-   **Methods:**
    -   `__init__(...)`: Calls the parent class constructor and initializes the interest rate.
    -   `apply_interest(self)`: Calculates and adds the interest to the account balance.
    -   `withdraw(self, amount)`: (Polymorphism) Overrides the `withdraw` method, not allowing the balance to become negative.

#### 👤 Customer Class (`src/customer.py`)

Represents a bank customer, who can have one or more accounts.

-   **Attributes:**
    -   `_name`: `str`.
    -   `_cpf`: `str` (Unique identifier for the customer).
    -   `_accounts`: `list` (Aggregation of `BankAccount` objects).
-   **Methods:**
    -   `add_account(self, account)`: Associates a new account with the customer.
    -   `remove_account(self, account_number)`: Removes an account from the customer's list.
    -   `list_accounts(self)`: Displays the details of all the customer's accounts.
    -   `find_account(self, account_number)`: Searches for and returns a specific account object.

#### 🏛️ Bank Class (`src/bank.py`)

The orchestrating class that manages the entire system, customers, and accounts.

-   **Attributes:**
    -   `_customers`: `list` (Aggregation of `Customer` objects).
-   **Methods:**
    -   `add_customer(self, customer)`: Adds a new customer, avoiding CPF duplication.
    -   `find_customer(self, cpf)`: Searches for and returns a customer object by their CPF.
    -   `create_account_for_customer(...)`: Creates and associates an account (`CheckingAccount` or `SavingsAccount`) with an existing customer.
    -   `perform_operation(self, account_number, operation_type, amount)`: Centralizes deposit and withdrawal operations.
    -   `display_all_customers_and_accounts(self)`: Generates a report of all customers and their respective accounts.

### ▶️ 4. Main Logic (`main.py`)

This is the application's entry point. It provides a simple command-line interface (CLI) for the user to interact with the banking system.

-   **Interaction Menu:** A `while` loop presents a menu with options such as:
    -   Add Customer
    -   Create Account
    -   Deposit
    -   Withdraw
    -   List Customer's Accounts
    -   Apply Interest (Savings)
    -   List All Customers
    -   Exit
-   **Operation Flow:** Captures user input and calls the appropriate methods of the `Bank` instance to perform the desired action.
-   **Input Handling:** Includes basic validations to ensure that the data entered by the user is consistent.

### 📖 5. Documentation and Execution

-   **Title:** Simple Banking System with Python and OOP
-   **Description:** What the project does and its objectives.
-   **Technologies:**
    -   Python 3.x
-   **OOP Concepts Applied:**
    -   **Encapsulation:** Protection of attributes with `_` and access via methods (getters).
    -   **Inheritance:** `CheckingAccount` and `SavingsAccount` inherit from `BankAccount`.
    -   **Polymorphism:** The `withdraw` method behaves differently in each type of account.
-   **How to Run:**
    1.  Clone the repository:
        ```sh
        git clone <YOUR_REPOSITORY_URL>
        ```
    2.  Navigate to the project folder:
        ```sh
        cd banking_system_oop
        ```
    3.  Run the main program:
        ```sh
        python main.py
        ```
-   **Author:** Your Name / GitHub Username

### ✨ 6. Evaluation and Refinement Criteria

The code was developed following best practices with a focus on the following points:

-   [✅] Correct Application of OOP Principles
-   [📂] Code Organization and Clarity
-   [✍️] Readability (Meaningful Names and Standards)
-   [🛡️] Basic Error Handling and Validations
-   [🚀] Functionality as Expected