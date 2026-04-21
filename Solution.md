# 📊 Superstore Sales Analysis — Solution

This section contains business-focused analysis using SQL along with insights.

---

## 1. Monthly Sales Trend

**Question:**  
How are sales changing over time?

**SQL Query:**  
Sales show an overall upward trend but with fluctuations, indicating inconsistent demand and possible seasonality.
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

**SQL Query:**
```sql
SELECT 
    Discount,
    round(SUM(Sales), 2) AS total_sales,
    round(SUM(Profit),2) AS total_profit
FROM Superstore
GROUP BY Discount
ORDER BY Discount;
```






