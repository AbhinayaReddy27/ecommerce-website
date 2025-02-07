**E-Commerce Platform Documentation**

Project Overview

This e-commerce platform is designed for Customers and Admins to handle shopping and management functionalities efficiently.

**1. User Section**

This section explains how users interact with the website.

**1.1. User Registration**

Users can create an account on the register.php page by providing their name, email, and password.

Registration allows access to personalized features like the shopping cart.

**1.2. User Login and Logout**

Login: Users log in on the login.php page using their registered email and password.

Logout: The logout.php page ends the session securely.

**1.3. Viewing Products**

All products are displayed on the homepage (index.php).

Users can view product names, prices, descriptions, and images.

**1.4. Adding Products to Cart**

On the index.php page, users click "Add to Cart" to save items.

The system records items in the cart for the logged-in user.

**1.5. Managing the Shopping Cart**

The cart.php page allows users to view, update, or remove items.

It displays the total cost of selected products.

**2. Admin Section**

This section explains how admins manage the platform.

**2.1. Admin Login and Logout**

Login: Admins log in via admin/login.php using their credentials.

Logout: The admin/logout.php page ends the session securely.

**2.2. Admin Dashboard**

The admin/dashboard.php page provides a control panel for management tasks.

**2.3. Adding Products**

The admin/add_product.php page allows admins to add new products.

Admins can fill out a form with product details and upload an image.

**2.4. Managing Products**

The admin/manage_products.php page displays all products in a table.

**Admins can:**

Edit product details.

Delete products from the store.

**3. Database Section**

This section explains the database structure.

**3.1. Users Table**

Stores information about all users (customers and admins):

Usernames, emails, hashed passwords.

Role field differentiating customers (user) and admins (admin).

**3.2. Products Table**

Contains product details:

Names, prices, descriptions, and image filenames.

**3.3. Cart Table**

Tracks items added to users' carts:

Links users to products.

Stores the quantity of each item.

**4. Website Flow**

This section explains user actions and system responses.

**4.1. User Registration**

Validates input, hashes password, and stores user data in the users table.

**4.2. User Login**

Verifies email and password, then starts a session.

**4.3. Adding a Product to Cart**

The system saves product details in the cart table, linked to the logged-in user.

**4.4. Admin Adding a Product**

Uploads product image and saves details in the products table.

Displays the new product on the homepage.

**4.5. Admin Deleting a Product**

Removes the product from the products table, making it unavailable.

**5. Security Measures**

**5.1. Password Security**

Passwords are hashed using password_hash() before storing in the database.

**5.2. Session Management**

Sessions track logged-in users using $_SESSION['user_id'] (customers) and $_SESSION['admin_id'] (admins).

**5.3. Securing Admin Access**

Admin login checks the role field in the users table to ensure only admins access the control pane



# ecommerce-website
**Step-by-Step Documentation for Database Setup**
Step 1: Creating the Database
Open phpMyAdmin or any database management tool.
Create a new database named ecommerce.
Run the following SQL commands to create the necessary tables:
Cart Table

CREATE TABLE cart (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
Products Table

CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    description TEXT,
    image VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
Users Table

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    role ENUM('user', 'admin') DEFAULT 'user'
);
Step 2: Setting Up db.php
Create a folder named includes in your project directory.
Inside this folder, create a file named db.php.
Add the following code:
db.php

<?php
$host = 'localhost';
$dbname = 'ecommerce';
$user = 'root';
$password = '';

try {
    $conn = new PDO("mysql:host=$host;dbname=$dbname", $user, $password);
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
?>
Explanation:

This script uses the PDO (PHP Data Objects) method for connecting to the database.
If the connection fails, an error message will be displayed.
Step 3: Testing the Database Connection
Create a new file named test_db.php in the root folder.
Add the following code to test the connection:
test_db.php

<?php
include 'includes/db.php';

if ($conn) {
    echo "Database connected successfully!";
} else {
    echo "Failed to connect to the database.";
}
?>
Access http://localhost/ecommerce/test_db.php in your browser.
Ensure the message "Database connected successfully!" is displayed.
