# 🍽️ Restaurant Billing System

A console-based **Restaurant Billing System** written in **C++17** using Object-Oriented Programming.
It manages a menu and customers, takes orders, generates GST bills and accepts **Cash / Card / UPI** payments.
All data is stored in text files, so it is still there after the program is closed and reopened.

| | |
|---|---|
| **Student Name** | Jenil Nagpara |
| **Enrollment No.** | IU2541230046 |
| **Project Code** | CPP27 - C++ Guided Project |
| **Semester** | 3 |
| **Language** | C++17 |

---

## 📌 Problem Statement
Small restaurants often prepare bills manually. This causes calculation mistakes, forgotten GST, lost customer and order details, and no summary of sales. This project solves it with a menu-driven program that converts an order into a correct GST bill, records the payment, produces a sales report and saves everything in files.

## ✨ Features
- **Add / Display / Search / Update / Delete** records (menu items and customers)
- **Main transaction:** Order → Bill (5% GST) → Payment
- **Payment modes:** Cash (with change), Card (16 digits, only last 4 stored), UPI (`name@bank`)
- **Sales report:** revenue, GST, pending amount, revenue by payment mode, item-wise sales, best seller, top customer
- **File persistence:** data loads at start-up and saves on exit (or from the menu)
- **Input validation** and **custom exception classes**, so the program never crashes on bad input

## 🧠 C++ / OOP Concepts Used
| Concept | Where it is used |
|---|---|
| Classes & Objects | 12 classes, e.g. `Order`, `Bill`, `Customer` |
| Encapsulation | Private/protected data with getters and validating setters |
| Constructors | Default and parameterized constructors in every class; copy constructor in `Order` |
| Destructors | Virtual destructors in `MenuItem` and `Payment`; `~Order()` frees its arrays |
| Inheritance | `MenuItem → FoodItem, BeverageItem`; `Payment → CashPayment, CardPayment, UpiPayment` |
| Runtime Polymorphism | `menu[i]->display()` and `payment->processPayment()` through base pointers |
| Dynamic Memory | `new` / `new[]` / `delete[]`; arrays double when full; Rule of Three in `Order` |
| File Handling | `FileManager` with `save()` and `load()` |
| Validation | `InputHelper` asks again until input is valid |
| Exception Handling | `BillingException` and 5 derived classes with `try / catch` |

## 📁 Repository Structure
```
Project_Source_Code/   all .cpp / .h files, Makefile, build.bat, Data/, tests/
UML_Diagrams/          use case, class and sequence diagrams
Screenshots/           program output screenshots
```

## ⚙️ How to Build and Run
Open the `Project_Source_Code` folder in a terminal.

**Windows (MinGW):** run `build.bat`, or:
```
g++ -std=c++17 -Wall -Wextra -O2 main.cpp InputHelper.cpp MenuItem.cpp Customer.cpp Order.cpp Bill.cpp Payment.cpp FileManager.cpp RestaurantSystem.cpp -o RestaurantBilling.exe
RestaurantBilling.exe
```
**Linux / macOS:**
```
make
./RestaurantBilling
```

## ▶️ How to Use
```
1. Add Record          5. Delete Record
2. Display Records     6. Main Transaction (Order -> Bill -> Payment)
3. Search Record       7. Report
4. Update Record       8. Save / Load
                       9. Exit (saves automatically)
```
**Quick demo:** choose `6` → `1` → customer ID `1001` → add items (`0` to finish) → bill is printed → choose a payment mode.

## 💰 Billing Formula
```
Subtotal    = sum of (quantity x unit price)
GST (5%)    = Subtotal x 0.05
Grand Total = Subtotal + GST
```
Example: 2 x Paneer Tikka (Rs. 250) + 1 x Cold Coffee (Rs. 110) = Rs. 610.00 + GST Rs. 30.50 = **Rs. 640.50**

## 💾 Data Files
| File | Content |
|---|---|
| `menu.txt` | Menu items (F = food, B = beverage) |
| `customers.txt` | Customers |
| `orders.txt` | Orders with item lines |
| `bills.txt` | Bills |
| `payments.txt` | Payments (C = cash, D = card, U = UPI) |

## ✅ Validation Rules
- Item name 2-30 characters, unique; price Rs. 1 to Rs. 10000
- Customer name 2-30 letters; phone 10 digits starting with 6-9, unique
- Quantity 1-50; card number 16 digits; UPI ID `name@bank`
- A customer with unpaid bills cannot be deleted; a paid order cannot be cancelled

## 🧪 Testing
17 automated test cases (15 required + 2 extra) in `Project_Source_Code/tests/run_tests.py`:
```
cd Project_Source_Code/tests
python3 run_tests.py ../RestaurantBilling
```
All 17 pass, also under AddressSanitizer and LeakSanitizer (no memory errors or leaks).

---

## 📐 UML Diagrams

### Use Case Diagram
![Use Case Diagram](UML_Diagrams/Use_Case_Diagram.png)

### Class Diagram
![Class Diagram](UML_Diagrams/Class_Diagram.png)

### Sequence Diagram 1 - Main Transaction
![Sequence Diagram 1 - Main Transaction](UML_Diagrams/Sequence_Diagram_1_Main_Transaction.png)

### Sequence Diagram 2 - Process Payment
![Sequence Diagram 2 - Process Payment](UML_Diagrams/Sequence_Diagram_2_Process_Payment.png)

---

## 🖼️ Screenshots

### 1. Start-up, main menu and Display Records
![Start-up, main menu and Display Records](Screenshots/01_Startup_Main_Menu_and_Display_Menu.png)

### 2. Add menu item (invalid prices rejected)
![Add menu item (invalid prices rejected)](Screenshots/02_Add_Menu_Item_With_Validation.png)

### 3. Add customer (invalid phone rejected)
![Add customer (invalid phone rejected)](Screenshots/03_Add_Customer_With_Validation.png)

### 4. Search menu item by name
![Search menu item by name](Screenshots/04_Search_Menu_Item_By_Name.png)

### 5. Search: NotFoundException handled
![Search: NotFoundException handled](Screenshots/05_Search_Not_Found_Exception.png)

### 6. Update menu item price
![Update menu item price](Screenshots/06_Update_Menu_Item_Price.png)

### 7. Delete menu item
![Delete menu item](Screenshots/07_Delete_Menu_Item.png)

### 8. Main transaction: order and generated bill
![Main transaction: order and generated bill](Screenshots/08_Main_Transaction_Order_And_Bill.png)

### 9. Cash payment with change
![Cash payment with change](Screenshots/09_Cash_Payment_Success.png)

### 10. Insufficient cash: PaymentException and retry
![Insufficient cash: PaymentException and retry](Screenshots/10_Cash_Payment_Exception_And_Retry.png)

### 11. Card payment validation
![Card payment validation](Screenshots/11_Card_Payment_Validation.png)

### 12. UPI payment validation
![UPI payment validation](Screenshots/12_UPI_Payment_Validation.png)

### 13. Sales report
![Sales report](Screenshots/13_Sales_Report.png)

### 14. Program reopened: data loaded from files
![Program reopened: data loaded from files](Screenshots/14_Restart_Data_Loaded_From_File.png)

### 15. Customers, orders, bills and payments after restart
![Customers, orders, bills and payments after restart](Screenshots/15_Persistence_Customers_Orders_Bills_Payments.png)

### 16. Data files created by FileManager
![Data files created by FileManager](Screenshots/16_Data_Files_Created.png)

### 17. Build with no warnings and 17/17 tests passed
![Build with no warnings and 17/17 tests passed](Screenshots/17_Build_And_Automated_Test_Results.png)

---

## ⚠️ Limitations
- Console only, no graphical interface; plain text storage; single user
- GST fixed at 5%, no discounts; payments are simulated (no real gateway)

## 🚀 Future Scope
- GUI or web front end, SQLite database, login roles, discounts and PDF receipts

## 👨‍💻 Author
**Jenil Nagpara** - Enrollment No. **IU2541230046**
