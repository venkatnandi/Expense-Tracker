import json
from datetime import datetime

# Initialize an empty list to store expenses
expenses = []

# Initialize an empty set to store expense categories
expense_categories = set()

# Function to add an expense
def add_expense():
    date = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    amount = float(input("Enter the expense amount: "))
    category = input("Enter the expense category (e.g., groceries, transportation, entertainment): ")
    description = input("Enter a brief description: ")

    expense = {
        "date": date,
        "amount": amount,
        "category": category,
        "description": description
    }

    expenses.append(expense)
    
    # Add the category to the set of expense categories
    expense_categories.add(category)
    
    print("Expense added successfully!")

# Function to list expenses
def list_expenses():
    if not expenses:
        print("No expenses recorded yet.")
    else:
        print("List of Expenses:")
        for idx, expense in enumerate(expenses, start=1):
            print(f"{idx}. Date: {expense['date']}, Amount: ${expense['amount']:.2f}, Category: {expense['category']}, Description: {expense['description']}")

# Function to list expense categories
def list_categories():
    if not expense_categories:
        print("No expense categories recorded yet.")
    else:
        print("Expense Categories:")
        for category in expense_categories:
            print(f"- {category}")

# Function to calculate total expenses for a specified time frame
def calculate_total_expenses(time_frame):
    total = 0
    today = datetime.now()
    
    for expense in expenses:
        expense_date = datetime.strptime(expense['date'], "%Y-%m-%d %H:%M:%S")
        
        if time_frame == 'daily' and expense_date.date() == today.date():
            total += expense['amount']
        elif time_frame == 'weekly' and today.isocalendar()[1] == expense_date.isocalendar()[1]:
            total += expense['amount']
        elif time_frame == 'monthly' and today.month == expense_date.month and today.year == expense_date.year:
            total += expense['amount']
    
    return total

# Function to generate and display a monthly report
def generate_monthly_report():
    today = datetime.now()
    current_month = today.strftime("%B %Y")
    report = {}
    
    for expense in expenses:
        expense_date = datetime.strptime(expense['date'], "%Y-%m-%d %H:%M:%S")
        
        if current_month not in report:
            report[current_month] = {}
        
        if expense['category'] not in report[current_month]:
            report[current_month][expense['category']] = 0
        
        if today.month == expense_date.month and today.year == expense_date.year:
            report[current_month][expense['category']] += expense['amount']
    
    print(f"Monthly Report ({current_month}):")
    
    for month, categories in report.items():
        print(f"\n{month}:")
        for category, total in categories.items():
            print(f"- Category: {category}, Total: ${total:.2f}")

# Function to save expenses to a JSON file
def save_expenses():
    with open("expenses.json", "w") as file:
        json.dump(expenses, file)

# Function to load expenses from a JSON file
def load_expenses():
    try:
        with open("expenses.json", "r") as file:
            data = json.load(file)
            expenses.extend(data)
            
            # Update the set of expense categories based on loaded data
            for expense in expenses:
                expense_categories.add(expense["category"])
    except FileNotFoundError:
        pass

# Load existing expenses when starting the application
load_expenses()

# Main menu
while True:
    print("\nExpense Tracker Menu:")
    print("1. Add Expense")
    print("2. List Expenses")
    print("3. List Expense Categories")
    print("4. Calculate Total Expenses (Daily/Weekly/Monthly)")
    print("5. Generate Monthly Report")
    print("6. Quit")
    
    choice = input("Enter your choice: ")

    if choice == "1":
        add_expense()
        save_expenses()
    elif choice == "2":
        list_expenses()
    elif choice == "3":
        list_categories()
    elif choice == "4":
        time_frame = input("Enter time frame (daily/weekly/monthly): ").lower()
        total = calculate_total_expenses(time_frame)
        print(f"Total expenses for the {time_frame} time frame: ${total:.2f}")
    elif choice == "5":
        generate_monthly_report()
    elif choice == "6":
        print("Exiting Expense Tracker. Have a good day!")
        break
    else:
        print("Invalid choice. Please try again.")
