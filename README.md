library-management
Library Management System Database

A complete MySQL database for managing library operations, including:  
- **Book cataloging** (titles, authors, genres, publishers)  
- **Member management** (registrations, memberships)  
- **Loan tracking** (checkouts, returns, due dates)  
- **Reservations system**  
- **Fines calculation** for overdue items  
- **Staff accounts** with role-based access  

Designed with proper **relational integrity**, constraints (PK, FK, CHECK), and optimized for real-world library workflows.  

---

## Setup Instructions  

### 1. Prerequisites  
- MySQL Server (8.0+)  
- MySQL Workbench or command-line client  

### 2. Database Installation  
```bash
# Clone the repository (if applicable)
git clone https://github.com/yourusername/library-management-db.git
cd library-management-db

# Import the SQL file
mysql -u root -p < library_schema.sql
```

### 3. Manual Setup (Alternative)  
1. Create the database:  
   ```sql
   CREATE DATABASE library_management;
   USE library_management;
   ```
2. Execute all SQL commands from [`library_schema.sql`](library_schema.sql)  

Key Relationships:  
- **1-to-Many**: Members → Loans, Books → Loans  
- **Many-to-Many**: Members ↔ Books (via Reservations)  
- **1-to-1**: Staff ↔ User Accounts  

---

Repository Contents  
- 📄 `library_schema.sql` - Complete SQL schema with sample data  
- 📄 `README.md` - This documentation  
- 🖼️ `library_erd.png` - Visual ER diagram  
- 📂 `queries/` - Example SQL queries for common operations  

---

Example Queries  
**1. Check overdue books:**  
```sql
SELECT m.first_name, b.title, l.due_date 
FROM loans l
JOIN members m ON l.member_id = m.member_id
JOIN books b ON l.book_id = b.book_id
WHERE l.status = 'Active' AND l.due_date < CURDATE();
```

**2. Find available books by genre:**  
```sql
SELECT b.title, a.first_name, a.last_name, g.name AS genre
FROM books b
JOIN authors a ON b.author_id = a.author_id
JOIN genres g ON b.genre_id = g.genre_id
WHERE b.available_copies > 0;
```
