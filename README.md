# Manila Classico — Barbershop Reservation & Queue Management System

## 📌 Overview
**Manila Classico** is a **Java Swing-based desktop application** designed to modernize barbershop operations with an **Apple-inspired** clean and minimal interface.  
It allows **Admins** and **Barbers** to manage bookings, queues, sales, and customer records efficiently, while providing a premium user experience.

## 🎯 Features
### **Admin Role**
- 📊 **Dashboard Widgets**:
  - Total Bookings
  - Total Sales
  - Scheduled Reservations
  - Total Customers
- 🗂 **Navigation Menu**:
  - Dashboard
  - Reservation
  - Services
  - Profiles
  - Customers
  - Sales
  - Reports
  - Support
- 👤 **User & Role Display** with Sign Out
- 📅 **Queue Management**:
  - Live Queue view
  - Scheduled Reservations view
  - Quick filters for status

### **Barber Role**
- View assigned queue
- Update status of appointments (Start / Finish)

## 🛠 Technology Stack
- **Language:** Java (JDK 17+ recommended)
- **Framework:** Java Swing (NetBeans GUI Builder)
- **Database:** MySQL (via JDBC)
- **Design Style:** Apple/macOS-inspired (clean, minimal, modern typography)

## 🗄 Database Schema
The application uses a **simple MySQL schema** for managing reservations, users, and services.

**Tables:**
- `users` — Stores login credentials and roles (Admin / Barber)
- `services` — Service catalog with prices and durations
- `reservations` — Customer bookings with time, barber, and status
- `customers` — Customer contact information
- `sales` — Sales records linked to reservations

**Sample SQL Setup:**
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    role ENUM('Admin', 'Barber') NOT NULL
);

CREATE TABLE services (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    duration INT NOT NULL
);

CREATE TABLE customers (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    contact_number VARCHAR(20),
    email VARCHAR(100)
);

CREATE TABLE reservations (
    id INT AUTO_INCREMENT PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL,
    contact_number VARCHAR(20),
    barber_id INT,
    service_id INT,
    date DATE NOT NULL,
    start_time TIME NOT NULL,
    end_time TIME NOT NULL,
    status ENUM('Scheduled', 'Waiting', 'Ongoing', 'Done', 'Canceled') NOT NULL,
    FOREIGN KEY (barber_id) REFERENCES users(id),
    FOREIGN KEY (service_id) REFERENCES services(id)
);

CREATE TABLE sales (
    id INT AUTO_INCREMENT PRIMARY KEY,
    reservation_id INT,
    amount DECIMAL(10,2) NOT NULL,
    date DATE NOT NULL,
    FOREIGN KEY (reservation_id) REFERENCES reservations(id)
);
```

## 📂 Project Structure
```
ManilaClassico/
├── src/
│   ├── gui/          # Java Swing UI forms
│   ├── model/        # Data models (POJOs)
│   ├── dao/          # Database access objects
│   ├── util/         # Utility classes (e.g., DB connection)
│   └── Main.java     # Application entry point
├── assets/           # Fonts, icons, resources
├── README.md         # Project documentation
└── LICENSE           # License file
```

## 🚀 Getting Started
### **Prerequisites**
- Java JDK 17 or later
- MySQL Server
- NetBeans IDE (or any Java IDE)
- MySQL Connector/J (JDBC driver)

### **Installation**
1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-username/manila-classico.git
   cd manila-classico
   ```

2. **Set Up the Database**
   - Create a new MySQL database (e.g., `manila_classico`)
   - Import the SQL schema provided above

3. **Configure Database Connection**
   - Edit `DBConnection.java` with your MySQL credentials:
     ```java
     private static final String URL = "jdbc:mysql://localhost:3306/manila_classico";
     private static final String USER = "root";
     private static final String PASSWORD = "your_password";
     ```

4. **Run the Application**
   - Open the project in NetBeans
   - Build & Run

## 🎨 Design Guidelines
- **Typography:** Modern, sans-serif fonts (e.g., SF Pro, Helvetica Neue)
- **Color Palette:** Neutral grays, subtle gradients, and accent colors inspired by Apple UI
- **UI Components:** Rounded corners, minimal borders, smooth hover effects

## 📌 Status
This project is currently in **active development**. Future updates will include:
- Enhanced filtering options for queues
- Role-based authentication improvements
- Additional reporting features

## 🤝 Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss your ideas.

## 📜 License
This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---
**Manila Classico** — Elevating the barbershop experience with premium, minimalist design.
