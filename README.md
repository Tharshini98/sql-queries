# sql-queries

CREATE DATABASE ecommerce;

CREATE TABLE customers(
id INT PRIMARY KEY IDENTITY(1,1),
name VARCHAR(50),
email VARCHAR(50),
address VARCHAR(255)
);

CREATE TABLE orders(
id INT PRIMARY KEY IDENTITY(1,1),
customer_id INT,
order_date DATE,
total_amount DECIMAL(10,2),
FOREIGN KEY(customer_id) REFERENCES customers(id)
);

CREATE TABLE products(
id INT PRIMARY KEY IDENTITY(1,1),
name VARCHAR(100),
price DECIMAL(10,2),
description
);

order_items Table

CREATE TABLE order_items(
id INT PRIMARY KEY AUTO_INCREMENT,
order_id INT,
product_id INT,
quantity INT
FOREIGN KEY(order_id) REFERENCES orders(id),
FOREIGN KEY(product_id) REFERENCES products(id)
);

1. SELECT name FROM customers
    JOIN orders ON customers.id = orders.customer_id
    WHERE orders.order_date >= CURDATE() - INTERVAL 30 day;
   --select customers name by joining orders who placed order within last 30 days

2. SELECT name, SUM(total_amount) AS total
FROM customers
JOIN orders ON customers.id = orders.customer_id
GROUP BY customers.id;
-- Get each customer's name and the total amount they have spent across all orders

3. UPDATE products
SET price = 45.00
WHERE name = "C";
-- Update the price of Product C to 45.00

4. ALTER TABLE products
ADD discount DECIMAL(10,2);
-- Add a new 'discount' column to the 'products' table

5. SELECT name, price 
FROM products
ORDER BY price DESC
LIMIT 3;
-- Get the 3 most expensive products based on price

6. SELECT name FROM customers
JOIN orders ON customers.id = order.customer_id
JOIN orders_items ON order.id = order_items.id
JOIN products ON order_items.product_id = product.id
WHERE products.name = "A";
-- Get names of customers who have ordered Product A
   
7. SELECT name AS customer_name , order_date
FROM customers
JOIN orders ON customers.id = order.customer_id;
-- Show each order with the customer’s name and the date it was placed

8. SELECT * FROM orders
WHERE total_amount > 150.00;
-- Select all orders where the total amount is greater than 150.00

9. CREATE TABLE order_items(
id INT PRIMARY KEY AUTO_INCREMENT,
order_id INT,
product_id INT,
quantity INT
FOREIGN KEY(order_id) REFERENCES orders(id),
FOREIGN KEY(product_id) REFERENCES products(id)
);
-- Create 'order_items' table to map multiple products to a single order

10. SELECT AVG (total_amount) 
FROM orders;
-- Calculate the average total amount of all orders in the system


