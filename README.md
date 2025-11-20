# IDC Pizza Sales Analysis — SQL Mini Project

### 📅 21 Days SQL Challenge — Indian Data Club × DPDZero  
### 👩‍💻 Completed by: **Shefali Uday Deshpande**  
### 🏆 Achieved: **14-Day Learning Streak Badge**

---

## 📖 **Project Overview**
This mini SQL project analyzes the **IDC Pizza Dataset** to understand sales patterns, pricing behavior, order activity, and category performance.  
The project is structured into 3 major phases involving database inspection, filtering, and sales analytics using SQL.

This project was completed as part of the  
**21 Days SQL Challenge by Indian Data Club × DPDZero**

---

## **Dataset Information**

The database contains the following tables:

| Table | Description |
|-------|-------------|
| **pizzas** | Pizza sizes & prices |
| **pizza_types** | Pizza names, categories & ingredients |
| **orders** | Order dates & timestamps |
| **order_details** | Quantity and pizza breakdown per order |

---

##  **Phase 1 — Foundation & Inspection**

### ✔ List unique pizza categories
```sql
SELECT DISTINCT category FROM pizza_types;
```

### ✔ Replace NULL ingredients with 'Missing Data'
```sql
SELECT pizza_type_id, name, COALESCE(ingredients, 'Missing Data') AS ingredients
FROM pizza_types
LIMIT 5;
```

### ✔ Find pizzas missing price
```sql
SELECT * FROM pizzas
WHERE price IS NULL;
```

---

##  **Phase 2 — Filtering & Data Exploration**

### ✔ Orders on a given date
```sql
SELECT * FROM orders
WHERE date = '2015-01-01';
```

### ✔ Pizzas priced between $15–$17
```sql
SELECT * FROM pizzas
WHERE price BETWEEN 15 AND 17;
```

### ✔ Pizzas containing the word "Chicken"
```sql
SELECT * FROM pizza_types
WHERE name ILIKE '%chicken%';
```

### ✔ Orders on '2015-02-15' OR after 8 PM
```sql
SELECT *
FROM orders
WHERE date = '2015-02-15'
   OR CAST(time AS TIME) >= '20:00:00';
```

---

##  **Phase 3 — Sales Performance Analysis**

### ✔ Total quantity of pizzas sold
```sql
SELECT SUM(quantity) AS total_quantity
FROM order_details;
```

### ✔ Average pizza price
```sql
SELECT AVG(price) AS average_price
FROM pizzas;
```

### ✔ Total order value per order
```sql
SELECT od.order_id,
       SUM(od.quantity * p.price) AS order_total
FROM order_details od
JOIN pizzas p ON od.pizza_id = p.pizza_id
GROUP BY od.order_id
ORDER BY order_total DESC;
```

### ✔ Quantity sold per category
```sql
SELECT pt.category,
       SUM(od.quantity) AS total_quantity
FROM order_details od
JOIN pizzas p ON od.pizza_id = p.pizza_id
JOIN pizza_types pt ON p.pizza_type_id = pt.pizza_type_id
GROUP BY pt.category
ORDER BY total_quantity DESC;
```

### ✔ Categories selling more than 5000 pizzas
```sql
SELECT pt.category,
       SUM(od.quantity) AS total_quantity
FROM order_details od
JOIN pizzas p ON od.pizza_id = p.pizza_id
JOIN pizza_types pt ON p.pizza_type_id = pt.pizza_type_id
GROUP BY pt.category
HAVING SUM(od.quantity) > 5000;
```

### ✔ Pizzas never ordered
```sql
SELECT p.*
FROM pizzas p
LEFT JOIN order_details od ON p.pizza_id = od.pizza_id
WHERE od.pizza_id IS NULL;
```

### ✔ Price difference between sizes (SELF JOIN)
```sql
SELECT a.pizza_type_id,
       a.size AS size_a,
       a.price AS price_a,
       b.size AS size_b,
       b.price AS price_b,
       (b.price - a.price) AS price_difference
FROM pizzas a
JOIN pizzas b
  ON a.pizza_type_id = b.pizza_type_id
 AND a.size <> b.size
ORDER BY a.pizza_type_id;
```

---

##  **Key Insights**

-  **Total pizzas sold:** 49,574  
-  **Average pizza price:** $16.44  
-  **Best-selling category:** Classic  
-  **Highest order value:** $444.20  
-  **Pizzas never ordered:** 5  
-  **Typical price difference (S → L):** $6–$8  

---

##  **Conclusion**
This project demonstrates real SQL problem-solving skills including joins, filtering, aggregate analysis, and data interpretation.  
It highlights how SQL can reveal important business insights from raw transactional data.

---

##  **Tech Stack**
-  MySQL  
-  MySQL Workbench  

---

## You can also view my LinkedIn post about this project here:  [LinkedIn Post](https://www.linkedin.com/posts/shefali-deshpande_sql-dataanalytics-dataindianclub-activity-7397279877177188353-6zeY?utm_source=share&utm_medium=member_desktop&rcm=ACoAAFoARdYBKv5OtRUiWKqHyNsqmH2IRlY5WmY)

##  Challenge Credits
**21 Days SQL Challenge  
Indian Data Club × DPDZero**

#SQL #DataAnalytics #IDC #DPDZero #MiniProject #SQLWithIDC

