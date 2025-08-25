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
SELECT COUNT(DISTINCT order_id) AS total_orders
FROM orders_details;
```

**Key Insight:**
*A brief sentence explaining the total number of orders found.*

**Visualization:**
*(Replace `path/to/your/image.png` with the actual path to your chart or table image in the repository)*
![Total Orders Chart](path/to/your/image1.png)

### 2. Calculate the total revenue generated from pizza sales.

**SQL Query:**
```sql
SELECT ROUND(SUM(quantity*price),2) AS Total_Revenue 
FROM order_details
JOIN pizzas
ON order_details.pizza_id = pizzas.pizza_id;
```

**Key Insight:**
*A brief sentence stating the total revenue generated.*

**Visualization:**
![Total Revenue Chart](path/to/your/image2.png)

### 3. Identify the highest-priced pizza.

**SQL Query:**
```sql
SELECT pizza_types.name,(pizzas.price) FROM pizzas
JOIN pizza_types ON
pizza_types.pizza_type_id = pizzas.pizza_type_id
ORDER BY price DESC LIMIT 1;
```

**Key Insight:**
*A brief sentence naming the highest-priced pizza and its cost.*

**Visualization:**
![Highest Priced Pizza](path/to/your/image3.png)

### 4. Identify the most common pizza size ordered.

**SQL Query:**
```sql
SELECT  pizzas.size, count(order_details.order_detail_id) AS order_count 
FROM order_details
JOIN pizzas ON
pizzas.pizza_id = order_details.pizza_id
GROUP BY size ORDER BY order_count DESC;
```

**Key Insight:**
*A brief sentence identifying the most frequently ordered pizza size.*

**Visualization:**
![Most Common Pizza Size](path/to/your/image4.png)

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

**Key Insight:**
*A brief summary of the top 5 most popular pizzas.*

**Visualization:**
![Top 5 Pizzas](path/to/your/image5.png)

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

**Key Insight:**
*A brief sentence highlighting which pizza categories are the most and least popular.*

**Visualization:**
![Quantity by Category](path/to/your/image6.png)

### 2. Determine the distribution of orders by hour of the day.

**SQL Query:**
```sql
SELECT HOUR(order_time) AS Hourly_order, count(order_id) AS order_count FROM orders
GROUP BY Hourly_order;
```

**Key Insight:**
*A brief summary of the peak and off-peak hours for pizza orders.*

**Visualization:**
![Hourly Order Distribution](path/to/your/image7.png)

### 3. Find the category-wise distribution of pizzas.

**SQL Query:**
```sql
SELECT category, count(name) FROM pizza_types
GROUP BY category;
```

**Key Insight:**
*A brief sentence explaining the variety of pizzas available in each category.*

**Visualization:**
![Category-wise Pizza Distribution](path/to/your/image8.png)

### 4. Calculate the average number of pizzas ordered per day.

**SQL Query:**
```sql
SELECT AVG(quantity) FROM
(SELECT orders.order_date, SUM(order_details.quantity) AS Quantity FROM orders
JOIN order_details ON
orders.order_id = order_details.order_id
GROUP BY orders.order_date) AS order_quantity;
```

**Key Insight:**
*A brief sentence stating the average number of pizzas sold daily.*

**Visualization:**
![Average Pizzas Per Day](path/to/your/image9.png)

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

**Key Insight:**
*A brief summary identifying the top 3 revenue-generating pizzas.*

**Visualization:**
![Top 3 Pizzas by Revenue](path/to/your/image10.png)

---



