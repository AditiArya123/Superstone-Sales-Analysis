# 📊 Superstore Sales Analysis — Solution

This section contains business-focused analysis using SQL along with insights.

---

## 1. Monthly Sales Trend

**Question:**  
How are sales changing over time?

```sql
SELECT 
    substr("Order Date", -4) || '-' || 
    printf('%02d', CAST(substr("Order Date", 1, instr("Order Date", '/') - 1) AS INTEGER)) AS month,
    SUM(Sales) AS revenue
FROM Superstore
GROUP BY month
ORDER BY month;
```

## 2. Impact of Discount on Profit

**Question:**
How does discount affect profitability?

```sql
SELECT 
    Discount,
    round(SUM(Sales), 2) AS total_sales,
    round(SUM(Profit),2) AS total_profit
FROM Superstore
GROUP BY Discount
ORDER BY Discount;
```

## 3. Loss-Making Products

**Question:**  
Which products are generating losses?

```sql
SELECT 
    product_name, 
    round(SUM(Sales), 2) AS total_sales,
    ABS(round(SUM(Profit),2)) AS total_loss
FROM Superstore
GROUP BY product_name
having total_profit < 0
ORDER BY total_profit asc
limit 10;
```

## 4. Category vs Profitability
**Question:**  
Which categories are most profitable, not just highest in sales?

```sql
SELECT 
    category, 
    round(SUM(Sales), 2) AS total_sales,
    round(SUM(Profit),2) AS total_profit
FROM Superstore
GROUP BY category
ORDER BY total_profit desc;
```

## 5. Regional Profitability

**Question:**  
Which regions are most profitable?

```sql
SELECT 
    region, 
    round(SUM(Sales), 2) AS total_sales,
    round(SUM(Profit),2) AS total_profit
FROM Superstore
GROUP BY region
ORDER BY total_profit desc;
```

## 6.Customer Concentration (Top Customers)

**Question:**  
How concentrated is revenue among top 10 customers?

```sql
SELECT 
    customer_name, 
    round(SUM(Sales), 2) AS total_spent
FROM Superstore
GROUP BY customer_name
ORDER BY total_spent desc
limit 10;
```

## 7. Customer Ranking
**Question:**  
How do customers rank based on their spending?

```sql
SELECT 
    customer_name, 
    round(SUM(Sales), 2) AS total_spent,
    rank() over (ORDER BY SUM(Sales) desc) as rank
FROM Superstore
GROUP BY customer_name;
```
