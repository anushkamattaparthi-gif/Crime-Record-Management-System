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

☕code:

import javax.swing.;
import javax.swing.table.DefaultTableModel;
import java.awt.;
import java.awt.event.*;
import java.io.FileWriter;
import java.util.ArrayList;

public class CRMS_GUI extends JFrame {

private final ArrayList<CrimeRecord> records = new ArrayList<>();  
private final DefaultTableModel tableModel;  
private final JTable table;  

private final JTextField tfName, tfAge, tfGender, tfCrime, tfStatus, tfOfficer, tfLocation, tfDate;  

// Search components  
private final JTextField tfSearch;  

public CRMS_GUI() {  
    super("Crime Record Management System (CRMS)");  
    setDefaultCloseOperation(EXIT_ON_CLOSE);  
    setSize(900, 650);  
    setLayout(new BorderLayout(10, 10));  

    // ==== Top Input Panel ====  
    JPanel inputPanel = new JPanel(new GridLayout(2, 8, 5, 5));  
    tfName = new JTextField(); tfAge = new JTextField(); tfGender = new JTextField();  
    tfCrime = new JTextField(); tfStatus = new JTextField();  
    tfOfficer = new JTextField(); tfLocation = new JTextField(); tfDate = new JTextField();  

    inputPanel.add(new JLabel("Criminal Name:")); inputPanel.add(tfName);  
    inputPanel.add(new JLabel("Age:")); inputPanel.add(tfAge);  
    inputPanel.add(new JLabel("Gender:")); inputPanel.add(tfGender);  
    inputPanel.add(new JLabel("Crime Type:")); inputPanel.add(tfCrime);  

    inputPanel.add(new JLabel("Case Status:")); inputPanel.add(tfStatus);  
    inputPanel.add(new JLabel("Officer Name:")); inputPanel.add(tfOfficer);  
    inputPanel.add(new JLabel("Location:")); inputPanel.add(tfLocation);  
    inputPanel.add(new JLabel("Date (YYYY-MM-DD):")); inputPanel.add(tfDate);  

    add(inputPanel, BorderLayout.NORTH);  

    // ==== Center Table ====  
    String[] cols = {"Case ID", "Criminal", "Age", "Gender", "Crime", "Status", "Officer", "Location", "Date"};  
    tableModel = new DefaultTableModel(cols, 0);  
    table = new JTable(tableModel);  
    add(new JScrollPane(table), BorderLayout.CENTER);  

    // ==== Search Panel ====  
    JPanel searchPanel = new JPanel(new FlowLayout(FlowLayout.LEFT, 10, 5));  
    tfSearch = new JTextField(20);  
    JButton searchBtn = new JButton("Search");  
    JButton resetBtn = new JButton("Reset");  

    searchPanel.add(new JLabel("Search:"));  
    searchPanel.add(tfSearch);  
    searchPanel.add(searchBtn);  
    searchPanel.add(resetBtn);  

    add(searchPanel, BorderLayout.WEST);  

    // ==== Bottom Buttons ====  
    JPanel btnPanel = new JPanel(new FlowLayout(FlowLayout.CENTER, 10, 5));  
    JButton addBtn = new JButton("Add Record");  
    JButton delBtn = new JButton("Delete Record");  
    JButton updateBtn = new JButton("Update Status");  
    JButton saveBtn = new JButton("Save to File");  
    JButton exitBtn = new JButton("Exit");  

    btnPanel.add(addBtn);  
    btnPanel.add(delBtn);  
    btnPanel.add(updateBtn);  
    btnPanel.add(saveBtn);  
    btnPanel.add(exitBtn);  
    add(btnPanel, BorderLayout.SOUTH);  

    // ==== Button Listeners ====  
    addBtn.addActionListener(e -> addRecord());  
    delBtn.addActionListener(e -> deleteRecord());  
    updateBtn.addActionListener(e -> updateStatus());  
    saveBtn.addActionListener(e -> saveToFile());  
    exitBtn.addActionListener(e -> System.exit(0));  

    searchBtn.addActionListener(e -> searchRecord());  
    resetBtn.addActionListener(e -> resetSearch());  

    setLocationRelativeTo(null);  
    setVisible(true);  
}  

// ===== Add Record =====  
private void addRecord() {  
    try {  
        String name = tfName.getText();  
        int age = Integer.parseInt(tfAge.getText());  
        String gender = tfGender.getText();  
        String crime = tfCrime.getText();  
        String status = tfStatus.getText();  
        String officer = tfOfficer.getText();  
        String location = tfLocation.getText();  
        String date = tfDate.getText();  

        CrimeRecord r = new CrimeRecord(name, age, gender, crime, status, officer, location, date);  
        records.add(r);  

        tableModel.addRow(new Object[]{  
                r.caseId, r.name, r.age, r.gender, r.crimeType,  
                r.caseStatus, r.officer, r.location, r.date  
        });  

        clearInputs();  
        JOptionPane.showMessageDialog(this, "Record Added!");  
    } catch (NumberFormatException ex) {  
        JOptionPane.showMessageDialog(this, "Age must be a number!", "Error", JOptionPane.ERROR_MESSAGE);  
    }  
}  

// ===== Delete Record =====  
private void deleteRecord() {  
    int row = table.getSelectedRow();  
    if (row >= 0) {  
        records.remove(row);  
        tableModel.removeRow(row);  
        JOptionPane.showMessageDialog(this, "Record Deleted!");  
    } else {  
        JOptionPane.showMessageDialog(this, "Select a record first!");  
    }  
}  

// ===== Update Status =====  
private void updateStatus() {  
    int row = table.getSelectedRow();  
    if (row >= 0) {  
        String newStatus = JOptionPane.showInputDialog(this, "Enter new status:");  
        if (newStatus != null && !newStatus.trim().isEmpty()) {  
            tableModel.setValueAt(newStatus, row, 5);  
            records.get(row).caseStatus = newStatus;  
            JOptionPane.showMessageDialog(this, "Status Updated!");  
        }  
    } else {  
        JOptionPane.showMessageDialog(this, "Select a record to update!");  
    }  
}  

// ===== Save to File =====  
private void saveToFile() {  
    try (FileWriter fw = new FileWriter("CrimeRecords_GUI.txt")) {  
        for (CrimeRecord r : records) {  
            fw.write(r.toString() + "\n");  
        }  
        JOptionPane.showMessageDialog(this, "Saved to CrimeRecords_GUI.txt");  
    } catch (Exception e) {  
        JOptionPane.showMessageDialog(this, "Error saving: " + e.getMessage());  
    }  
}  

// ===== Search Records =====  
private void searchRecord() {  
    String keyword = tfSearch.getText().toLowerCase();  
    if (keyword.isEmpty()) {  
        JOptionPane.showMessageDialog(this, "Enter search text!");  
        return;  
    }  

    tableModel.setRowCount(0); // clear table  

    for (CrimeRecord r : records) {  
        if (String.valueOf(r.caseId).contains(keyword) ||  
            r.name.toLowerCase().contains(keyword) ||  
            r.crimeType.toLowerCase().contains(keyword) ||  
            r.officer.toLowerCase().contains(keyword) ||  
            r.caseStatus.toLowerCase().contains(keyword)) {  

            tableModel.addRow(new Object[]{  
                    r.caseId, r.name, r.age, r.gender, r.crimeType,  
                    r.caseStatus, r.officer, r.location, r.date  
            });  
        }  
    }  
}  

// ===== Reset Search =====  
private void resetSearch() {  
    tfSearch.setText("");  
    tableModel.setRowCount(0);  
    for (CrimeRecord r : records) {  
        tableModel.addRow(new Object[]{  
                r.caseId, r.name, r.age, r.gender, r.crimeType,  
                r.caseStatus, r.officer, r.location, r.date  
        });  
    }  
}  

// ===== Clear Input Boxes =====  
private void clearInputs() {  
    tfName.setText(""); tfAge.setText(""); tfGender.setText(""); tfCrime.setText("");  
    tfStatus.setText(""); tfOfficer.setText(""); tfLocation.setText(""); tfDate.setText("");  
}  

// ===== Crime Record Class =====  
static class CrimeRecord {  
    static int counter = 1001;  
    int caseId;  
    String name, gender, crimeType, caseStatus, officer, location, date;  
    int age;  

    CrimeRecord(String name, int age, String gender, String crimeType,  
                String caseStatus, String officer, String location, String date) {  
        this.caseId = counter++;  
        this.name = name;  
        this.age = age;  
        this.gender = gender;  
        this.crimeType = crimeType;  
        this.caseStatus = caseStatus;  
        this.officer = officer;  
        this.location = location;  
        this.date = date;  
    }  

    @Override  
    public String toString() {  
        return "Case ID: " + caseId + ", " + name + " (" + crimeType + ") - " + caseStatus;  
    }  
}  

public static void main(String[] args) {  
    SwingUtilities.invokeLater(CRMS_GUI::new);  
}

}

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
