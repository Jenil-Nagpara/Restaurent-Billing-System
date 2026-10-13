# 🍽️ Restaurant Billing System

A console-based **Restaurant Billing System** written in **C++17** using Object-Oriented Programming.
It manages a menu and customers, takes orders, generates GST bills and accepts **Cash / Card / UPI** payments.
All data is stored in text files, so it is still there after the program is closed and reopened.

| | |
|---|---|
| **Student Name** | Jenil Nagpara |
| **Enrollment No.** | IU2541230046 |
| **Project Code** | CPP27 – C++ Guided Project |
| **Semester** | 3 |
| **Language** | C++17 |

---

## 📌 Problem Statement
Small restaurants often prepare bills manually. This causes calculation mistakes, forgotten GST, lost customer
and order details, and no summary of sales. This project solves it with a menu-driven program that converts an
order into a correct GST bill, records the payment, produces a sales report and saves everything in files.

## ✨ Features
- **Add / Display / Search / Update / Delete** records (menu items and customers)
- **Main transaction:** Order → Bill (5% GST) → Payment
- **Payment modes:** Cash (with change), Card (16 digits, only last 4 stored), UPI (`name@bank`)
- **Sales report:** revenue, GST collected, pending amount, revenue by payment mode, item-wise sales, best-selling item, top customer
- **File persistence:** data loads at start-up and saves on exit (or from the menu)
- **Input validation** on every field and **custom exception classes**, so the program never crashes on bad input

## 🧠 C++ / OOP Concepts Used
| Concept | Where it is used |
|---|---|
| Classes & Objects | 12 classes, e.g. `Order`, `Bill`, `Customer` |
| Encapsulation | Private/protected data with getters and validating setters |
| Constructors | Default and parameterized constructors in every class; copy constructor in `Order` |
| Destructors | Virtual destructors in `MenuItem` and `Payment`; `~Order()` frees its arrays |
| Inheritance | `MenuItem → FoodItem, BeverageItem`; `Payment → CashPayment, CardPayment, UpiPayment` |
| Runtime Polymorphism | `menu[i]->display()` and `payment->processPayment()` through base pointers |
| Dynamic Memory | `new` / `new[]` / `delete[]`; arrays double in size when full; Rule of Three in `Order` |
| File Handling | `FileManager` with `save()` and `load()` using `ofstream` / `ifstream` |
| Validation | `InputHelper` keeps asking until the input is valid |
| Exception Handling | `BillingException` and 5 derived classes with `try / catch` |

## 🗂️ Classes
| Class | Responsibility |
|---|---|
| `MenuItem` (abstract), `FoodItem`, `BeverageItem` | Menu entries |
| `Customer` | Customer details |
| `Order` | One customer's order (dynamic arrays of item lines) |
| `Bill` | GST calculation and invoice printing |
| `Payment` (abstract), `CashPayment`, `CardPayment`, `UpiPayment` | Payment modes |
| `FileManager` | Saving and loading all data files |
| `RestaurantSystem` | Controller: owns the data and implements every menu option |

## 📁 Project Structure
```
Project_Source_Code/
├── main.cpp                  Menu loop only
├── RestaurantSystem.h/.cpp   Controller class
├── MenuItem.h/.cpp           MenuItem, FoodItem, BeverageItem
├── Customer.h/.cpp
├── Order.h/.cpp
├── Bill.h/.cpp
├── Payment.h/.cpp            Payment, CashPayment, CardPayment, UpiPayment
├── FileManager.h/.cpp
├── InputHelper.h/.cpp        Validated input
├── BillingException.h        Custom exceptions
├── Data/                     menu.txt, customers.txt, orders.txt, bills.txt, payments.txt
├── tests/run_tests.py        Automated test cases
├── Makefile
└── build.bat
UML_Diagrams/                 Use case, class and sequence diagrams
Screenshots/                  Program output screenshots
```

## ⚙️ How to Build and Run

**Windows (MinGW):** double-click `build.bat`, or run:
```
g++ -std=c++17 -Wall -Wextra -O2 main.cpp InputHelper.cpp MenuItem.cpp Customer.cpp Order.cpp Bill.cpp Payment.cpp FileManager.cpp RestaurantSystem.cpp -o RestaurantBilling.exe
RestaurantBilling.exe
```

**Linux / macOS:**
```
make
./RestaurantBilling
```
Run the program from inside the `Project_Source_Code` folder so it can find the `Data/` folder.

## ▶️ How to Use
```
1. Add Record          5. Delete Record
2. Display Records     6. Main Transaction (Order -> Bill -> Payment)
3. Search Record       7. Report
4. Update Record       8. Save / Load
                       9. Exit (saves automatically)
```
**Quick demo:** choose `6` → `1` → enter customer ID `1001` → add items (enter `0` to finish) → the bill is printed → choose a payment mode.

On the very first run (no `Data/menu.txt`) a sample menu of 12 items is created automatically.

## 💰 Billing Formula
```
Subtotal    = sum of (quantity x unit price)
GST (5%)    = Subtotal x 0.05
Grand Total = Subtotal + GST
```
Example: 2 x Paneer Tikka (Rs. 250) + 1 x Cold Coffee (Rs. 110) = Rs. 610.00, GST Rs. 30.50, **Total Rs. 640.50**

## 💾 Data Files
Records are stored one per line, with fields separated by `|`.

| File | Content |
|---|---|
| `menu.txt` | Menu items (F = food, B = beverage) |
| `customers.txt` | Customers |
| `orders.txt` | Orders with their item lines |
| `bills.txt` | Bills |
| `payments.txt` | Payments (C = cash, D = card, U = UPI) |

The full card number is never saved, only the last 4 digits.

## ✅ Validation Rules
- Item name: 2–30 characters; price: Rs. 1 to Rs. 10000; item names must be unique
- Customer name: 2–30 letters; phone: 10 digits starting with 6–9, and unique
- Quantity: 1–50 per item
- Card number: 16 digits; UPI ID: `name@bank`
- A customer with unpaid bills cannot be deleted, and a paid order cannot be cancelled

## 🧪 Testing
17 automated test cases (15 required + 2 extra) are in `tests/run_tests.py`:
```
cd tests
python3 run_tests.py ../RestaurantBilling
```
All 17 pass. The suite was also run with AddressSanitizer and LeakSanitizer, with no memory errors or leaks.

## 📐 UML Diagrams
| Diagram | File |
|---|---|
| Use Case Diagram | `UML_Diagrams/Use_Case_Diagram.png` |
| Class Diagram | `UML_Diagrams/Class_Diagram.png` |
| Sequence Diagram 1 (Main Transaction) | `UML_Diagrams/Sequence_Diagram_1_Main_Transaction.png` |
| Sequence Diagram 2 (Process Payment) | `UML_Diagrams/Sequence_Diagram_2_Process_Payment.png` |

![Use Case Diagram](UML_Diagrams/Use_Case_Diagram.png)
![Class Diagram](UML_Diagrams/Class_Diagram.png)

## 🖼️ Screenshots
![Main Menu](Screenshots/01_Startup_Main_Menu_and_Display_Menu.png)
![Bill](Screenshots/08_Main_Transaction_Order_And_Bill.png)
![Report](Screenshots/13_Sales_Report.png)

## ⚠️ Limitations
- Console only, no graphical interface
- Plain text storage, single user
- GST fixed at 5%, no discounts
- Payments are simulated (no real payment gateway)

## 🚀 Future Scope
- GUI or web front end
- Database (SQLite) instead of text files
- Login with cashier / manager roles
- Discounts, loyalty points, PDF receipts

## 👨‍💻 Author
**Jenil Nagpara** – Enrollment No. **IU2541230046**
