Retrieve the total number of orders placed:
code
SELECT COUNT(*) AS total_orders FROM Orders;

Calculate the total revenue generated from pizza sales:
code
SELECT SUM(price * quantity) AS total_revenue FROM Orders;

Identify the highest-priced pizza:
code
SELECT pizza_name, MAX(price) AS highest_price FROM Pizzas;

Identify the most common pizza size ordered:
code
SELECT size, COUNT(size) AS size_count 
FROM Orders 
GROUP BY size 
ORDER BY size_count DESC 
LIMIT 1;

List the top 5 most ordered pizza types along with their quantities:
code
SELECT pizza_name, SUM(quantity) AS total_quantity 
FROM Orders 
GROUP BY pizza_name 
ORDER BY total_quantity DESC 
LIMIT 5;

Intermediate Queries:

Join the necessary tables to find the total quantity of each pizza category ordered:

code
SELECT P.category, SUM(O.quantity) AS total_quantity
FROM Orders O
JOIN Pizzas P ON O.pizza_id = P.pizza_id
GROUP BY P.category;

Determine the distribution of orders by hour of the day:
code
SELECT HOUR(order_time) AS order_hour, COUNT(*) AS total_orders
FROM Orders
GROUP BY order_hour
ORDER BY order_hour;

Join relevant tables to find the category-wise distribution of pizzas:
code
SELECT P.category, COUNT(O.order_id) AS total_orders
FROM Orders O
JOIN Pizzas P ON O.pizza_id = P.pizza_id
GROUP BY P.category;

Group the orders by date and calculate the average number of pizzas ordered per day:
code
SELECT DATE(order_time) AS order_date, AVG(quantity) AS avg_pizzas_per_day
FROM Orders
GROUP BY order_date;

Determine the top 3 most ordered pizza types based on revenue:
code
SELECT pizza_name, SUM(price * quantity) AS total_revenue
FROM Orders
GROUP BY pizza_name
ORDER BY total_revenue DESC
LIMIT 3;

Advanced Queries:
Calculate the percentage contribution of each pizza type to total revenue:
code
SELECT pizza_name, 
(SUM(price * quantity) / (SELECT SUM(price * quantity) FROM Orders) * 100) AS revenue_percentage
FROM Orders
GROUP BY pizza_name;

Analyze the cumulative revenue generated over time:
code
SELECT order_date, 
SUM(SUM(price * quantity)) OVER (ORDER BY order_date) AS cumulative_revenue
FROM Orders
GROUP BY order_date;

Determine the top 3 most ordered pizza types based on revenue for each pizza category:
code
SELECT P.category, O.pizza_name, SUM(O.price * O.quantity) AS total_revenue
FROM Orders O
JOIN Pizzas P ON O.pizza_id = P.pizza_id
GROUP BY P.category, O.pizza_name
ORDER BY P.category, total_revenue DESC
LIMIT 3;


# Pizza Order Management System

## Project Overview
The Pizza Order Management System is built using MySQL to track and analyze pizza sales. It retrieves key insights like the total number of orders placed, total revenue, top-ordered pizzas, and more.

## Features

### Basic Features:
- **Total Orders Placed:** Retrieve the total number of orders placed in the system.
- **Total Revenue:** Calculate the total revenue generated from pizza sales.
- **Highest-Priced Pizza:** Identify the most expensive pizza.
- **Most Common Pizza Size:** Find the most ordered pizza size.
- **Top 5 Most Ordered Pizza Types:** List the most popular pizza types along with their order quantities.

### Intermediate Features:
- **Pizza Category Quantities:** Retrieve the total quantity of pizzas ordered in each category.
- **Orders by Hour:** Analyze the distribution of orders placed by the hour.
- **Category-Wise Distribution:** Find the number of orders for each pizza category.
- **Average Orders Per Day:** Calculate the average number of pizzas ordered per day.
- **Top 3 Pizzas by Revenue:** Determine the top 3 pizzas based on revenue.

### Advanced Features:
- **Revenue Contribution:** Calculate each pizza type's contribution to total revenue.
- **Cumulative Revenue:** Track the cumulative revenue generated over time.
- **Top 3 Pizzas by Revenue Per Category:** Retrieve the top 3 pizzas based on revenue for each pizza category.

## Database Schema

- **Orders Table:**
  - `order_id`: Primary key.
  - `pizza_id`: Foreign key from the Pizzas table.
  - `quantity`: Number of pizzas ordered.
  - `price`: Price of the pizza.
  - `order_time`: Timestamp for when the order was placed.

- **Pizzas Table:**
  - `pizza_id`: Primary key.
  - `pizza_name`: Name of the pizza.
  - `category`: Type/category of the pizza (e.g., Veg, Non-Veg).
  - `price`: Price of the pizza.
 
  - ## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/pizza-order-management.git
