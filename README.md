# Crime-Record-Management-System
Java Swing-based Crime Record Management System for adding, searching, updating, deleting, and saving crime records with a user-friendly graphical interface.
Crime Record Management System

A  Swing-based Crime Record Management System (CRMS) designed to manage crime records through a simple and user-friendly graphical interface. The application allows users to add, search, update, delete, view, and save crime records using Java Swing components.

📌 Project Overview

The Crime Record Management System provides a desktop-based interface for maintaining basic crime and case information.

Each record contains:

- Case ID
- Criminal Name
- Age
- Gender
- Crime Type
- Case Status
- Officer Name
- Location
- Date

The application uses an "ArrayList" to temporarily store records during program execution and provides file handling functionality to save records to a text file.

✨ Features

📝 Add Crime Record

Users can enter crime and criminal details through the input fields and add a new record to the system.

🔍 Search Records

Records can be searched using:

- Case ID
- Criminal Name
- Crime Type
- Officer Name
- Case Status

✏️ Update Case Status

Users can select a record from the table and update its case status.

🗑️ Delete Record

A selected crime record can be deleted from the system.

💾 Save Records

Crime records can be saved to a text file named:

"CrimeRecords_GUI.txt"

🆔 Automatic Case ID

Each new record receives an automatically generated Case ID starting from 1001.

📊 Tabular Display

All records are displayed in a JTable for easy viewing and management.

⚠️ Input Validation

The application validates the age field and displays an error message if a non-numeric value is entered.

🛠️ Technologies Used

- Java
- Java Swing
- Java AWT
- JTable
- ArrayList
- FileWriter
- Event Handling

🏗️ Project Structure

Crime-Record-Management-System/
│
├── CRMS_GUI.java
│
└── CrimeRecords_GUI.txt

«"CrimeRecords_GUI.txt" is generated when the Save to File option is used.»

🖥️ Application Interface

The graphical interface contains:

1. Input Panel – Enter criminal and case information.
2. Records Table – Displays stored crime records.
3. Search Panel – Search existing records.
4. Action Buttons – Add, delete, update, save, and exit.

⚙️ How to Run

Prerequisites

Make sure Java Development Kit (JDK) is installed on your computer.

Check your Java installation using:

java -version
javac -version

Step 1: Clone the Repository

git clone https://github.com/YOUR-USERNAME/Crime-Record-Management-System.git

Step 2: Open the Project Folder

cd Crime-Record-Management-System

Step 3: Compile the Program

javac CRMS_GUI.java

Step 4: Run the Application

java CRMS_GUI

The Crime Record Management System window will open.

📖 How to Use

1. Add a Record

Enter the required information:

Criminal Name
Age
Gender
Crime Type
Case Status
Officer Name
Location
Date

Click Add Record.

The system automatically generates a Case ID.

2. Search for a Record

Enter a keyword in the search box and click Search.

The system searches the available records by Case ID, criminal name, crime type, officer, or case status.

3. Update Status

Select a record from the table and click Update Status.

Enter the new case status when prompted.

4. Delete a Record

Select a record and click Delete Record.

5. Save Records

Click Save to File to save the records to:

CrimeRecords_GUI.txt

6. Reset Search

Click Reset to display all available records again.

💾 Data Storage

The current version uses:

- "ArrayList<CrimeRecord>" for in-memory record storage.
- "FileWriter" for saving records to a text file.

The application does not currently use a database such as MySQL.

🔄 Program Workflow

Start Application
       ↓
Enter Crime Details
       ↓
Add Record
       ↓
Generate Case ID
       ↓
Display Record in Table
       ↓
 ┌─────┼──────────┐
 ↓     ↓          ↓
Search Update    Delete
 ↓     ↓          ↓
View   Change    Remove
       Status
       ↓
Save Records to File
       ↓
Exit

🚀 Future Enhancements

The project can be further improved by adding:

- MySQL or other database integration
- Admin login and authentication
- Separate user roles
- FIR management
- Criminal history management
- Advanced filtering and sorting
- Date validation
- Input validation for all fields
- Export records to CSV/PDF
- Automatic report generation
- Database backup and recovery
- Improved modern GUI design

🔐 Current Limitations

- Records are stored only in memory while the application is running.
- The text file stores a simplified representation of each record.
- Data is not persistent in a database.
- There is currently no login or authentication system.
- Date input is accepted as text and is not strictly validated.

🎓 Academic Project

This project was developed as a Java desktop application to demonstrate concepts including:

- Object-Oriented Programming
- Java Swing GUI development
- Event-driven programming
- ArrayList and data management
- JTable
- Exception handling
- File handling
- Basic CRUD operations
- Search functionality

👩‍💻 Author

Anushka

GitHub: "@anushkamattaparthi-gif"

📄 License

This project is intended for educational and academic purposes.
