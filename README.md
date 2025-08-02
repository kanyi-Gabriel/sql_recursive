# 🎧 SQL Practice – Day (Chinook Database)

## 📌 Overview
This project captures my progress in the SQL learning journey using the **Chinook SQLite database**.  
For this day, I explored **advanced database features** such as **triggers** and **correlated subqueries** to handle more complex data relationships.

---

## 🗂️ Database Used
- **Chinook SQLite** (available at [Chinook Database GitHub](https://github.com/lerocha/chinook-database))

---

## ✅ Concepts Practiced on Day 6
- 🔹 **Triggers** → Automate actions when certain database events occur  
- 🔹 **Correlated Subqueries** → Dynamic filtering based on row-level comparisons  
- 🔹 **CTEs** → Annual genre growth rate 
- 🔹 **Advanced CASE Statements** → Categorizing data based on conditions  
- 🔹 **Combining Multiple Features** → Using CTE + CASE + aggregation in a single query  

---

## 🧠 Business Questions Answered
1. **Log events whenever a new invoice is inserted using a trigger.**  
2. **Find customers who spent more than the average spending of their country (correlated subquery).**  
3. **Display the full employee hierarchy with levels using a recursive CTE.**  
4. **Classify customers into spending tiers (Silver, Gold, Platinum) using CASE.**  
5. **Determine the top genre per country and label it accordingly.**

---

## 💻 Sample Query (Recursive CTE for Employee Hierarchy)
```sql
SELECT 
    FirstName || " " || LastName as Customer_Name,
    sum(i.Total) as Total_spent,
    CASE 
        WHEN  sum(i.Total) > 45 THEN  "Platinum"
        WHEN  sum(i.Total) BETWEEN 40 and 45 THEN  "Gold"
        ELSE "silver"
    END as Customer_Tier 
FROM customers c
JOIN
    invoices i
ON
    c.CustomerId = i.CustomerId
GROUP BY c.CustomerId
ORDER BY Total_spent DESC


