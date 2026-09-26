
📘 PROJECT-1 — SQL Database Practice
A simple and easy-to-understand README based only on the given PDF.

🌟 Project Overview
This project contains SQL practice for a simple Customer Order Management System.

It works with 4 main tables:

#	Table	Purpose
1️⃣	Customers	Stores customer information

2️⃣	Orders	Stores customer orders

3️⃣	Products	Stores product information

4️⃣	OrderDetails	Connects orders with products

👤 1. CUSTOMERS TABLE
The Customers table stores basic customer details.

🏗️ Create Table

CREATE TABLE Customers
(
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Email VARCHAR(100) UNIQUE,
    Address VARCHAR(100)
);
📌 Important Points
CustomerID → Primary Key

Name → Cannot be empty (NOT NULL)

Email → Must be unique (UNIQUE)

Address → Stores customer address

➕ Insert Customer Data
INSERT INTO Customers (CustomerID, Name, Email, Address)
VALUES

(101, 'Alice Sharma', 'alice@gmail.com', 'Ahmedabad'),

(102, 'Rahul Patel', 'rahul@gmail.com', 'Surat'),

(103, 'Priya Shah', 'priya@gmail.com', 'Vadodara'),

(104, 'Riya Mehta', 'riya@gmail.com', 'Rajkot'),

(105, 'Jay Patel', 'jay@gmail.com', 'Anand');
🔍 Display All Customers

SELECT * FROM Customers;

✏️ Update Customer Address
UPDATE Customers

SET Address = 'Gandhinagar'
WHERE CustomerID = 101;

❌ Delete a Customer
DELETE FROM Customers
WHERE CustomerID = 105;

🔎 Find a Specific Customer
SELECT * FROM Customers
WHERE Name = 'Alice Sharma';

🛒 2. ORDERS TABLE
The Orders table stores information about customer orders.

🏗️ Create Table

CREATE TABLE Orders
(
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    TotalAmount DECIMAL(10,2),
    FOREIGN KEY (CustomerID)
    REFERENCES Customers(CustomerID)
    ON DELETE CASCADE
);
📌 Important Points
OrderID → Primary Key

CustomerID → Foreign Key

OrderDate → Stores order date

TotalAmount → Stores total order amount

ON DELETE CASCADE → Related orders are deleted when the referenced customer is deleted

➕ Insert Orders
INSERT INTO Orders (OrderID, CustomerID, OrderDate, TotalAmount)
VALUES

(1001, 101, '2026-09-01', 6000),

(1002, 102, '2026-09-05', 30000),

(1003, 101, '2026-09-10', 55000),

(1004, 103, '2026-09-15', 3500),

(1005, 104, '2026-09-20', 2500);

🔍 Orders of a Specific Customer

SELECT *
FROM Orders
WHERE CustomerID = 101;

💰 Calculate Total Order Amount

SELECT SUM(TotalAmount) AS Total_Order_Amount
FROM Orders;

❌ Delete an Order

DELETE FROM Orders
WHERE OrderID = 1005;

📅 Orders from Last 30 Days

SELECT *
FROM Orders
WHERE OrderDate >= CURDATE() - INTERVAL 30 DAY;

📊 Highest, Lowest & Average Order

SELECT
    MAX(TotalAmount) AS Highest_Order,
    MIN(TotalAmount) AS Lowest_Order,
    AVG(TotalAmount) AS Average_Order
FROM Orders;

💻 3. PRODUCTS TABLE

The Products table stores product information.

🏗️ Create Table

CREATE TABLE Products
(
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100) NOT NULL,
    Price DECIMAL(10,2),
    Stock INT
);

➕ Insert Product Data

INSERT INTO Products (ProductID, ProductName, Price, Stock)
VALUES

(201, 'Laptop', 55000, 10),

(202, 'Smartphone', 30000, 15),

(203, 'Headphones', 3500, 20),

(204, 'Keyboard', 2500, 25),

(205, 'Mouse', 1200, 0);

🔽 Sort Products by Price

SELECT *
FROM Products
ORDER BY Price DESC;
DESC means highest to lowest.


💵 Display Price of a Product

SELECT ProductName, Price
FROM Products
WHERE ProductName = 'Laptop';

❌ Delete Out-of-Stock Product
DELETE FROM Products
WHERE Stock = 0;

💰 Products Between ₹2500 and ₹5000

SELECT *
FROM Products
WHERE Price BETWEEN 2500 AND 5000;

📈 Find Maximum & Minimum Price

SELECT
    MAX(Price) AS Maximum_Price,
    MIN(Price) AS Minimum_Price
FROM Products;

📦 4. ORDERDETAILS TABLE
The OrderDetails table stores details about products included in orders.


🏗️ Create Table
CREATE TABLE OrderDetails
(
    OrderDetailID INT PRIMARY KEY,
    OrderID INT,
    ProductID INT,
    SubTotal DECIMAL(10,2),
    FOREIGN KEY (OrderID)
    REFERENCES Orders(OrderID)
    ON DELETE CASCADE,
    FOREIGN KEY (ProductID)
    REFERENCES Products(ProductID)
);

📌 Important Points

OrderDetailID → Primary Key

OrderID → Foreign Key connected to Orders

ProductID → Foreign Key connected to Products

SubTotal → Stores the subtotal

ON DELETE CASCADE is used with OrderID

➕ Insert Order Details
INSERT INTO OrderDetails
(OrderDetailID, OrderID, ProductID, SubTotal)
VALUES

(1, 1001, 203, 3500),

(2, 1001, 204, 2500),

(3, 1002, 202, 30000),

(4, 1003, 201, 55000),

(5, 1004, 203, 3500);

🔍 Details of a Specific Order

SELECT *
FROM OrderDetails
WHERE OrderID = 1001;

💰 Calculate Total Revenue

SELECT SUM(SubTotal) AS Total_Revenue
FROM OrderDetails;

🏆 Top 3 Most Ordered Products

SELECT
    ProductID,
    COUNT(*) AS Order_Count
FROM OrderDetails
GROUP BY ProductID
ORDER BY Order_Count DESC
LIMIT 3;

🔢 Count How Many Times Product 203 Was Sold

SELECT
    ProductID,
    COUNT(*) AS Times_Sold
FROM OrderDetails
WHERE ProductID = 203
GROUP BY ProductID;

⭐ SQL COMMANDS TO REMEMBER

Command	Easy Meaning

CREATE TABLE	Creates a new table

INSERT INTO	Adds data

SELECT	Displays data

UPDATE	Changes existing data

DELETE	Removes data

WHERE	Adds a condition

ORDER BY	Sorts data

GROUP BY	Groups data

LIMIT	Limits number of results

SUM()	Calculates total

MAX()	Finds maximum value

MIN()	Finds minimum value

AVG()	Finds average

COUNT()	Counts records

BETWEEN	Finds values in a range

DESC	Highest to lowest

FOREIGN KEY	Connects tables

PRIMARY KEY	Uniquely identifies a row

🧠 QUICK REVISION
🔑 Keys
Primary Key

Uniquely identifies a record.

Used in Customers, Orders, Products, and OrderDetails.

Foreign Key

Connects one table with another.

Used in Orders and OrderDetails.

📊 Aggregate Functions

SUM()   → Total

MAX()   → Highest

MIN()   → Lowest

AVG()   → Average

COUNT() → Count


🔍 Most Important Clauses

WHERE      → Condition

ORDER BY   → Sorting

GROUP BY   → Grouping

LIMIT      → Limit results

BETWEEN    → Range

🔗 TABLE RELATIONSHIP

Customers
    │
    │ CustomerID
    ▼
 Orders
    │
    │ OrderID
    ▼
OrderDetails
    ▲
    │ ProductID
    │
Products

Simple idea:

A customer can have orders.

An order can contain product details.

Products are stored separately.

OrderDetails connects orders and products.

🎯 PROJECT IN ONE LINE
Customers → Orders → OrderDetails ← Products

This project mainly practices creating tables, inserting data, retrieving data, updating data, deleting data, sorting, filtering, grouping, counting, and using 
