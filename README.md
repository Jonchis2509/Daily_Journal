# 📘 Daily Journal – Python Console App

This is a simple console-based daily journal application written in Python. The program allows users to write and store their thoughts each day in uniquely named files (based on the current date). It also lets users read previous entries.

This project is part of my **Python 50-Day Learning Challenge**, showcasing practical skills like file handling, working with directories, exception control, and modular programming.

---

## 🚀 Features

- 📝 Write a new journal entry with automatic filename based on the current date.
- 📖 Read all previous entries from the `entries/` folder.
- ❌ Basic error handling (e.g. missing folders or read/write issues).
- 📁 Creates an "entries" directory if it doesn't exist.
- 🧭 Easy-to-use menu interface.

---

## 🛠️ Technologies Used

- **Python 3**
- `datetime` module
- `os` module
- Exception handling (`try`, `except`, `finally`)
- Modular functions

---

## 📂 File Structure




import os
from datetime import datetime

#Function to display the principal menu and its options.
def menu():
    print("\n📘 DAILY JOURNAL MENU")
    print("1. Write new journal entry.")
    print("2. Read the past entries.")
    print("3. Exit.")
    #Requires user to choose an option from the menu
    return input("Choose an option: ")

#Funtion that write the entry in the file
def write_entry():
    today = datetime.now().strftime("%d-%m-%Y")
    filename = f"entries/entries of {today}.txt"
    entry = input(f"Write your journal entry of {today}: \n")

    try:
        with open(filename, "a") as file:
            file.write(entry + "\n")
        print(f"Entry of {today} saved.") #Message to confirm that the entry stored correctly.

    except IOError:
        print("Error writing file.") #Message if the file cannot find.

#Funtion to read the old entries
def read_entry():
    try:
        files = os.listdir("entries")
        if not files:
            print("No journal entries found.")
            return
        for f in files:
            with open(f"entries/{f}", "r") as file:
                print(file.read())
    except FileNotFoundError:
        print ("The entries folder doesn´t exist.") #Error message if the folder doesn´t exist
    except IOError: 
        print("Error reading file.")  #Error message if the file cannot read

if not os.path.exists("entries"):
    os.mkdir("entries")


#Loop to work the functions
while True:
    choice = menu()
    if choice == "1":
        write_entry()
    elif choice == "2":
        read_entry()
    elif choice == "3":
        print("Goodbye!")
        break
    else:
        print("Invalid choise.")
