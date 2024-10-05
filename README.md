# 📚 Library Management System - Calgary Central Library

## **Table of Contents**
- [📖 Introduction](#-introduction)
- [🎯 Mission](#-mission)
- [🎯 Objectives](#-objectives)
- [🛠 Database Design: Why It Matters](#-database-design-why-it-matters)
- [🔗 Relationships: How Tables Connect](#-relationships-how-tables-connect)
- [📝 ER Diagram](#-er-diagram)
- [📋 Table Breakdown](#-table-breakdown)
  - [🏢 Branch Table](#-branch)
  - [👩‍💼 Employee Table](#-employee)
  - [📚 Books Table](#-books)
  - [👤 Customer Table](#-customer)
  - [📄 IssueStatus Table](#-issuestatus)
  - [🔄 ReturnStatus Table](#-returnstatus)
  - [📅 EventAndProgramData Table](#-eventandprogramdata)
  - [🚚 Supplier Table](#-supplier)
- [🔍 Example Database Queries](#-example-database-queries)
- [✅ Conclusion](#-conclusion)

---

## **📖 Introduction**
The Calgary Central Library plays a key role in the community, offering a wide range of books, resources, and events to its members. As the library grows, a well-organized and efficient database system is essential to keep up with the increasing demands. This case study outlines the design of a library management system aimed at improving operations like catalog management, event coordination, and customer services.

## **🎯 Mission**
Our goal is to make a diverse selection of books and resources easily accessible to the Calgary community. This system is designed to streamline library operations, making it easier for staff and users alike to find what they need, attend events, and manage their library accounts.

## **🎯 Objectives**
- Effectively manage the book collection across multiple branches.
- Simplify customer registration and account management.
- Track book loans and returns with detailed statuses.
- Organize events and link them with specific employees and branches.
- Provide data reports for better library management and decision-making.

---

## **🛠 Database Design: Why It Matters**
This database design was created to automate key library tasks, helping the library staff manage their resources more efficiently and ensuring a better experience for users. The system is designed to scale with the library’s future needs, handling everything from book inventory to event planning.

Here’s a quick overview of the main tables in the database:
1. **Branch**: Stores details about each library branch.
2. **Employee**: Keeps track of staff members, their roles, and which branch they work at.
3. **Books**: Manages all information related to the books, including their availability.
4. **Customer**: Stores user data such as contact details and membership information.
5. **IssueStatus**: Tracks when books are borrowed and returned.
6. **ReturnStatus**: Records returns and any fines that may apply.
7. **EventAndProgramData**: Keeps a log of events and programs hosted by the library.
8. **Supplier**: Stores supplier details for book orders.

---

## **🔗 Relationships: How Tables Connect**
The relationships between these tables are crucial for ensuring smooth operations. For instance:
- **Books** and **Branches** are connected because each book is located at a specific branch.
- **Employees** are assigned to branches, creating a connection between the **Branch** and **Employee** tables.
- **Customers** borrow books, which is tracked by the **IssueStatus** and **ReturnStatus** tables.
- Events and programs are linked to both employees and branches through the **EventAndProgramData** table.

These relationships make sure that the system maintains accurate records and can handle multiple tasks at once, from loaning books to organizing events.

---

## **📝 ER Diagram**
The Entity-Relationship (ER) diagram provides a clear, visual representation of how all the tables in the database are related. It shows which tables are connected and the type of relationship (one-to-one, one-to-many, etc.) they share. This is an important tool for understanding how the database works and for ensuring the integrity of the data.


---

## **📋 Table Breakdown**

### **🏢 Branch**
Holds information about the different library locations.
- **BranchID**: Unique identifier for each branch.
- **BranchName**: Name of the branch.
- **Address**: Location of the branch.
- **Contact**: Phone number for the branch.

### **👩‍💼 Employee**
Stores staff information.
- **EmployeeID**: Unique ID for each staff member.
- **Name**: Employee's name.
- **Position**: Job title.
- **Salary**: Employee's salary.
- **BranchID**: Links to the branch where the employee works.
- **HiredDate**: Date when the employee was hired.

### **📚 Books**
Manages book inventory.
- **BookID**: Unique ID for each book.
- **Title**: Book title.
- **Author**: Name of the author.
- **ISBN**: International Standard Book Number.
- **PublishDate**: Date the book was published.
- **BranchID**: Links the book to its library branch.
- **SupplierID**: Connects the book to the supplier.

### **👤 Customer**
Tracks user information.
- **CustomerID**: Unique ID for each user.
- **Name**: Customer’s name.
- **Email**: Email address.
- **Phone**: Phone number.

### **📄 IssueStatus**
Tracks book loans.
- **IssueID**: Unique ID for each book issue.
- **BookID**: ID of the book being borrowed.
- **CustomerID**: ID of the customer borrowing the book.
- **IssueDate**: Date the book was issued.
- **DueDate**: Date the book is due for return.
- **Status**: Status of the book (borrowed, returned, etc.).

### **🔄 ReturnStatus**
Records book returns.
- **ReturnID**: Unique ID for each return.
- **IssueID**: Connects to the book issue.
- **ReturnDate**: Date the book was returned.
- **Fine**: Any fines associated with the late return.

### **📅 EventAndProgramData**
Stores information about library events.
- **EventID**: Unique ID for each event.
- **EventName**: Name of the event.
- **BranchID**: Links the event to the branch hosting it.
- **EmployeeID**: Links the event to the employee responsible for it.
- **Date**: Date the event is happening.
- **Description**: Brief description of the event.

### **🚚 Supplier**
Holds information about book suppliers.
- **SupplierID**: Unique ID for each supplier.
- **Name**: Supplier’s name.
- **Email**: Supplier’s email.
- **Phone**: Supplier’s contact number.

---

## **🔍 Example Database Queries**

Here are a few example queries that could be used to test the system’s functionality:

1. **Find books borrowed by a specific customer**:
   ```sql
   SELECT C.Name, B.Title, I.IssueDate 
   FROM Customer C 
   JOIN IssueStatus I ON C.CustomerID = I.CustomerID 
   JOIN Books B ON I.BookID = B.BookID 
   WHERE C.CustomerID = 1;
   ```

2. **List employees working in a specific branch**:
   ```sql
   SELECT E.Name, B.BranchName 
   FROM Employee E 
   JOIN Branch B ON E.BranchID = B.BranchID 
   WHERE B.BranchName = 'Downtown Branch';
   ```

3. **Count the total number of books available in each branch**:
   ```sql
   SELECT B.BranchName, COUNT(Bo.BookID) AS TotalBooks 
   FROM Branch B 
   JOIN Books Bo ON B.BranchID = Bo.BranchID 
   GROUP BY B.BranchName;
   ```

4. **Calculate the total fines collected from overdue books**:
   ```sql
   SELECT SUM(Fine) AS TotalFines 
   FROM ReturnStatus 
   WHERE Fine > 0;
   ```

---

## **✅ Conclusion**
This library management system database design is built to handle key functions like book inventory, event scheduling, and customer management. The ER diagram provides a strong foundation for understanding how each table interacts, and the relationships ensure the data is organized and easily accessible. The design ensures the library is ready to meet current demands and scale for future growth.

---
