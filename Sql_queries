--To create database

create database pizza_sales;


--To make it default schema
use pizza_sales;


--To retrieve the total number of orders placed.
SELECT 
    COUNT(order_id) AS total_orders
FROM
    orders;


--To calculate the total revenue generated from pizza sales.
SELECT 
    SUM(od.quantity * p.price) AS revenue
FROM
    order_details od
        JOIN
    pizzas p ON od.pizza_id = p.pizza_id;


--To identify the highest-priced pizza.
SELECT 
    pt.name, p.price
FROM
    pizza_types pt
        JOIN
    pizzas p ON pt.pizza_type_id = p.pizza_type_id
ORDER BY p.price DESC
LIMIT 1;


--To identify the most common (quantity) pizza size ordered.
SELECT 
    p.size, SUM(od.quantity) AS quantity
FROM
    order_details od
        JOIN
    pizzas p ON od.pizza_id = p.pizza_id
GROUP BY p.size
ORDER BY quantity DESC;


--To list the top 5 most ordered pizza types along with their quantities.
	SELECT 
    pt.name, SUM(od.quantity) AS quantity
FROM
    pizzas p
        JOIN
    pizza_types pt ON p.pizza_type_id = pt.pizza_type_id
        JOIN
    order_details od ON od.pizza_id = p.pizza_id
GROUP BY pt.name
ORDER BY quantity DESC
LIMIT 5;


--To join the necessary tables to find the total quantity of each pizza category ordered.
	SELECT 
    pt.category, SUM(od.quantity) AS quantity
FROM
    pizzas p
        JOIN
    pizza_types pt ON p.pizza_type_id = pt.pizza_type_id
        JOIN
    order_details od ON od.pizza_id = p.pizza_id
GROUP BY pt.category
ORDER BY quantity DESC;


--To determine the distribution of orders by hour of the day.
SELECT 
    HOUR(time) AS hour, COUNT(order_id) AS order_count
FROM
    orders
GROUP BY HOUR(time);


--To join relevant tables to find the category-wise distribution of pizzas.
SELECT 
    category, COUNT(name) AS name
FROM
    pizza_types
GROUP BY category;


--To group the orders by date and calculate the average number of pizzas ordered per day.
SELECT 
    ROUND(AVG(quantity), 0)
FROM
    (SELECT 
        o.date, SUM(od.quantity) AS quantity
    FROM
        orders o
    JOIN order_details od ON o.order_id = od.order_id
    GROUP BY o.date) AS average_quantity;


--To find the total revenue generated per month.
SELECT 
    DATE_FORMAT(o.date, '%Y-%M') AS month,
    SUM(od.quantity * p.price) AS revenue
FROM
    order_details od
        JOIN
    orders o ON o.order_id = od.order_id
        JOIN
    pizzas p ON od.pizza_id = p.pizza_id
GROUP BY month;


--To determine the top 3 most ordered pizza types based on revenue.
SELECT 
    pt.name, SUM(od.quantity * p.price) AS revenue
FROM
    pizzas p
        JOIN
    order_details od ON p.pizza_id = od.pizza_id
        JOIN
    pizza_types pt ON pt.pizza_type_id = p.pizza_type_id
GROUP BY pt.name
ORDER BY revenue ASC
LIMIT 3;


--To calculate the percentage contribution of each pizza type to total revenue.
SELECT 
    pt.category,
    ROUND((SUM(od.quantity * p.price) / (SELECT 
                    SUM(od.quantity * p.price) AS revenue
                FROM
                    order_details od
                        JOIN
                    pizzas p ON od.pizza_id = p.pizza_id) * 100),
            2) AS revenue
FROM
    pizza_types pt
        JOIN
    pizzas p ON p.pizza_type_id = pt.pizza_type_id
        JOIN
    order_details od ON od.pizza_id = p.pizza_id
GROUP BY pt.category
ORDER BY revenue DESC;
