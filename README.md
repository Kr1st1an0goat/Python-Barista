ND1's Barista v0.1

© 2025 Kr1st14n0. All rights reserved.

Project Overview

ND1's Barista v0.1 is a console-based coffee order simulation program developed by Kr1st14n0. Users can view a menu, place orders with quantities, calculate totals including tax, select a payment method, and save all order history to a structured JSON file. This project demonstrates Python fundamentals, data structures, file handling, and problem-solving skills, making it an excellent addition to a developer portfolio.

Features

Display a coffee menu with prices

Take multiple orders with quantities

Automatically calculate total price and tax (10% by default)

Save orders in a structured JSON file as a mini-database

Support multiple payment types: Cash, Card (Debit/Credit)

Assign unique order numbers for each order

Display a detailed order summary at the end

Python Code


import json
import os

# Define menu
menu = {
    "latte": 4.50,
    "espresso": 3.00,
    "americano": 3.50,
    "cappuccino": 4.00
}

# 1. Display welcome and menu
print("Welcome to ND1's Barista v0.1!")
print("Here’s the menu:")
for item, price in menu.items():
    print(f"- {item.title()}: ${price:.2f}")

# 2. Get customer name
name = input("Enter your name: ")

# 3. Take orders
order_items = {}
while True:
    choice = input("Enter a drink (or 'done' to finish): ").lower()
    if choice == "done":
        break
    if choice in menu:
        quantity = int(input(f"How many {choice}s? "))
        order_items[choice.title()] = order_items.get(choice.title(), 0) + quantity
    else:
        print("Sorry, we don’t have that. Try again.")

# 4. Calculate totals, tax, etc.
price = sum(menu[item.lower()] * qty for item, qty in order_items.items())
tax = round(price * 0.1, 2)
total_amount = round(price + tax, 2)

payment = input("Payment type (Card - Debit/Credit or Cash): ")

# 5. Handle JSON storage
if os.path.exists("orders.json"):
    with open("orders.json", "r") as file:
        try:
            all_orders = json.load(file)
        except json.JSONDecodeError:
            all_orders = []
else:
    all_orders = []

order_no = len(all_orders) + 1

order_data = {
    "Name": name,
    "Order No.": order_no,
    "Orders": order_items,
    "Price": round(price, 2),
    "Tax": tax,
    "Total Amount": total_amount,
    "Payment Type": payment
}

all_orders.append(order_data)

with open("orders.json", "w") as file:
    json.dump(all_orders, file, indent=4)

# 6. Print order summary
print("\nOrder Summary:")
print(f"Order No.: {order_no}")
print(f"Customer: {name}")
for item, qty in order_items.items():
    print(f"- {item} x {qty}")
print(f"Price: ${price:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Total Amount: ${total_amount:.2f}")
print(f"Payment: {payment}")
print("Thank you for your order!")

JSON Order Structure

Orders are stored in orders.json as a list of dictionaries. Each order contains:

Field	Description
Name	Customer's name
Order No.	Unique order number
Orders	Dictionary of items and quantities
Price	Total price before tax
Tax	Tax amount (10%)
Total Amount	Price + Tax
Payment Type	Cash or Card (Debit/Credit)

Example:

[
  {
    "Name": "Alice",
    "Order No.": 1,
    "Orders": {"Latte": 2, "Espresso": 1},
    "Price": 12.0,
    "Tax": 1.2,
    "Total Amount": 13.2,
    "Payment Type": "Card - Debit"
  }
]

Future Enhancements

Add timestamp to each order in the JSON database

Check for returning customers and greet them differently

Show prices next to each item in the billing (price × quantity)

Create separate JSON files for each day instead of storing all orders in one file

Generate receipt numbers for every order

Display a polished ending message before program exit

How to Run

Clone the repository:

git clone https://github.com/<your-username>/ND1s-Barista-v0.1.git


Navigate to the project folder:

cd ND1s-Barista-v0.1


Run the program:

python barista.py


Follow the on-screen prompts to place your order.



Author & Rights

Author: Kr1st14n0
Copyright: © 2025 Kr1st14n0. All rights reserved.
This project and all its code, documentation, and assets are the intellectual property of Kr1st14n0. Unauthorized copying, distribution, or commercial use is prohibited.
