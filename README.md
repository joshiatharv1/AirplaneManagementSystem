# Airline Management System - Admin Dashboard

## Overview

This project is a part of an **Airline Management System** that allows users to book flights, view bookings, and manage payment details. The **Admin Dashboard** provides the functionality for the admin to handle requests, including cancellation requests, and view important statistics related to bookings and payments.

### Features
1. **Admin Dashboard**: 
   - Displays a table of **cancellation requests** submitted by users.
   - Provides a **visualization** of important statistics using **JFreeChart**:
     - **Bookings per Flight**: Number of bookings for each flight.
     - **Payment Method Distribution**: Distribution of payment methods used by users (Credit Card, Debit Card, PayPal).
     - **Cancellation Request Count**: The number of cancellation requests made for each flight.

2. **Requests Table**: 
   - Displays all the **cancellation requests** made by users, including:
     - Request ID
     - User ID
     - Flight Number
     - Seat Number
     - Status
     - Request Type
     - Request Date

3. **Statistics**:
   - **Bookings per Flight**: A bar chart showing the number of bookings per flight.
   - **Payment Method Distribution**: A pie chart displaying the distribution of payment methods.
   - **Cancellation Request Count**: A bar chart showing the number of cancellation requests per flight.

4. **Interactive Dashboard**: 
   - Admin can interact with the system to view requests and statistics in real-time.

---

## Technologies Used
- **Java**: The main programming language used to develop the system.
- **JFreeChart**: Used for visualizing booking and payment statistics.
- **JDBC**: For connecting to the MySQL database and fetching flight, booking, payment, and request data.
- **MySQL**: Relational database used to store data related to flights, bookings, payments, and requests.
- **Swing**: Java's GUI toolkit used for building the user interface.

---

## Database Tables
The system uses the following MySQL tables:

### Users Table
Stores user details including name, email, and phone number.

```sql
CREATE TABLE Users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(150) NOT NULL UNIQUE,
    phone_number VARCHAR(15)
);

CREATE TABLE Flights (
    flight_id INT AUTO_INCREMENT PRIMARY KEY,
    flight_number VARCHAR(20) NOT NULL,
    origin VARCHAR(50) NOT NULL,
    destination VARCHAR(50) NOT NULL,
    departure_time DATETIME NOT NULL,
    arrival_time DATETIME NOT NULL,
    price DECIMAL(10, 2) NOT NULL
);

CREATE TABLE Bookings (
    booking_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    flight_id INT NOT NULL,
    booking_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    seat_number VARCHAR(10),
    status VARCHAR(20) DEFAULT 'confirmed',
    FOREIGN KEY (user_id) REFERENCES Users(user_id),
    FOREIGN KEY (flight_id) REFERENCES Flights(flight_id)
);
CREATE TABLE Payments (
    payment_id INT AUTO_INCREMENT PRIMARY KEY,
    booking_id INT NOT NULL,
    payment_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    amount DECIMAL(10, 2) NOT NULL,
    payment_method VARCHAR(20) NOT NULL,
    payment_status VARCHAR(20) DEFAULT 'success',
    FOREIGN KEY (booking_id) REFERENCES Bookings(booking_id)
);
CREATE TABLE Requests (
    request_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    flight_number VARCHAR(20) NOT NULL,
    seat_number VARCHAR(10),
    status VARCHAR(20),
    request_type VARCHAR(50) DEFAULT 'Cancellation Request',
    request_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);
```

