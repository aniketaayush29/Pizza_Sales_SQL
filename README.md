# Pizza Sales Analysis: SQL Insights

This repository showcases a comprehensive analysis of a pizza sales dataset using SQL. The goal of this project was to derive actionable insights by answering key business questions, ranging from basic sales metrics to more complex, intermediate-level queries.

---

## 📊 Project Structure

The analysis is divided into two main sections:

1.  **Basic Analysis:** High-level queries to understand overall performance and identify top sellers.
2.  **Intermediate Analysis:** Deeper-dive queries that involve joins and aggregations to uncover trends and patterns.

---

## 📈 Basic Analysis

### 1. Retrieve the total number of orders placed.

**SQL Query:**
```sql
SELECT COUNT(order_id) AS total_orders
FROM orders;
```

**OUTPUT:**

![imgae alt](https://github.com/aniketaayush29/Pizza_Sales_SQL/blob/main/images/img1.png?raw=true)

### 2. Calculate the total revenue generated from pizza sales.

**SQL Query:**
```sql
SELECT ROUND(SUM(quantity*price),2) AS Total_Revenue 
FROM order_details
JOIN pizzas
ON order_details.pizza_id = pizzas.pizza_id;
```


**OUTPUT:**
![!image alt](https://github.com/aniketaayush29/Pizza_Sales_SQL/blob/main/images/img2.png?raw=true)

### 3. Identify the highest-priced pizza.

**SQL Query:**
```sql
SELECT pizza_types.name,(pizzas.price) FROM pizzas
JOIN pizza_types ON
pizza_types.pizza_type_id = pizzas.pizza_type_id
ORDER BY price DESC LIMIT 1;
```

**OUTPUT:**
![!image alt](https://github.com/aniketaayush29/Pizza_Sales_SQL/blob/main/images/img3.png?raw=true)

### 4. Identify the most common pizza size ordered.

**SQL Query:**
```sql
SELECT  pizzas.size, count(order_details.order_detail_id) AS order_count 
FROM order_details
JOIN pizzas ON
pizzas.pizza_id = order_details.pizza_id
GROUP BY size ORDER BY order_count DESC;
```

**OUTPUT:**
![!image alt](https://github.com/aniketaayush29/Pizza_Sales_SQL/blob/main/images/img4.png?raw=true)

### 5. List the top 5 most ordered pizza types along with their quantities.

**SQL Query:**
```sql
SELECT pizza_types.name, SUM(order_details.quantity) AS Total_pizzas_ordered FROM pizza_types
JOIN pizzas ON
pizzas.pizza_type_id = pizza_types.pizza_type_id
JOIN order_details ON
order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_types.name
ORDER BY Total_pizzas_ordered DESC LIMIT 5;
```

**OUTPUT:**
![!image alt](https://github.com/aniketaayush29/Pizza_Sales_SQL/blob/main/images/img5.png?raw=true)

---

## 🚀 Intermediate Analysis

### 1. Find the total quantity of each pizza category ordered.

**SQL Query:**
```sql

SELECT pizza_types.category, SUM(order_details.quantity) AS Quantity FROM order_details
JOIN pizzas ON
pizzas.pizza_id = order_details.pizza_id
JOIN pizza_types ON
pizza_types.pizza_type_id = pizzas.pizza_type_id
GROUP BY pizza_types.category;
```

**OUTPUT:**
![!image alt](https://github.com/aniketaayush29/Pizza_Sales_SQL/blob/main/images/img6.png?raw=true)

### 2. Determine the distribution of orders by hour of the day.

**SQL Query:**
```sql
SELECT HOUR(order_time) AS Hourly_order, count(order_id) AS order_count FROM orders
GROUP BY Hourly_order;
```

**OUTPUT:**
![!image alt](https://github.com/aniketaayush29/Pizza_Sales_SQL/blob/main/images/img7.png?raw=true)

### 3. Find the category-wise distribution of pizzas.

**SQL Query:**
```sql
SELECT category, count(name) FROM pizza_types
GROUP BY category;
```

**OUTPUT:**
![!image alt](https://github.com/aniketaayush29/Pizza_Sales_SQL/blob/main/images/img8.png?raw=true)

### 4. Calculate the average number of pizzas ordered per day.

**SQL Query:**
```sql
SELECT AVG(quantity) FROM
(SELECT orders.order_date, SUM(order_details.quantity) AS Quantity FROM orders
JOIN order_details ON
orders.order_id = order_details.order_id
GROUP BY orders.order_date) AS order_quantity;
```

**OUTPUT:**
![!image alt](https://github.com/aniketaayush29/Pizza_Sales_SQL/blob/main/images/img9.png?raw=true)

### 5. Determine the top 3 most ordered pizza types based on revenue.

**SQL Query:**
```sql
SELECT pizza_types.name, sum(order_details.quantity*pizzas.price) AS revenue
FROM pizza_types
JOIN pizzas ON
pizzas.pizza_type_id = pizza_types.pizza_type_id
JOIN order_details ON
order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_types.name
ORDER BY revenue DESC LIMIT 3;
```

**OUTPUT:**
![!image alt](https://github.com/aniketaayush29/Pizza_Sales_SQL/blob/main/images/img10.png?raw=true)

---



