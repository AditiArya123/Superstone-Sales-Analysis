# 📊 Superstore Sales Analysis — Solution

This section contains business-focused analysis using SQL along with insights.

---

## 1. Monthly Sales Trend
**Result:**  
Monthly revenue values were generated showing variation over time.

**Insight:**  
Sales show an overall upward trend with fluctuations, indicating growth with seasonal demand patterns.

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
**Result:**  
Profitability was compared across different discount levels.

**Insight:**  
Higher discounts reduce profitability, and aggressive discounting can lead to losses.

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
**Result:**  
Products with negative total profit were identified.

**Insight:**  
Some products consistently lose money despite generating sales, suggesting pricing or cost issues.

**Question:**  
Which products are generating losses?

```sql
SELECT 
    product_name, 
    ROUND(SUM(Sales), 2) AS total_sales,
    ABS(ROUND(SUM(Profit), 2)) AS total_loss
FROM Superstore
GROUP BY product_name
HAVING SUM(Profit) < 0
ORDER BY total_loss DESC
LIMIT 10;
```

## 4. Category vs Profitability
**Result:**  
Sales and profit were compared across product categories.

**Insight:**  
Technology performs strongest overall, while some categories generate lower profit margins.

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
**Result:**  
Sales and profit performance were calculated for each region.

**Insight:**  
Regional demand differs significantly, indicating location-based opportunities and inefficiencies.

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

## 6. Top Customers & Ranking
**Result:**  
Customers were ranked based on cumulative purchases.

**Insight:**  
Revenue is unevenly distributed across customers, with top buyers outperforming the rest.

**Question:**  
Who are the highest-value customers and how do they rank based on spending?

**SQL Query:**
```sql
SELECT 
    "Customer Name",
    SUM(Sales) AS total_spent,
    RANK() OVER (ORDER BY SUM(Sales) DESC) AS rank
FROM orders
GROUP BY "Customer Name"
LIMIT 10;
Limit 10;
```

## 7. Customer Segment Profitability
**Result:**  
Total sales and profit were calculated for each customer segment.

**Insight:**  
Some segments generate strong revenue but lower profit margins, while others contribute healthier profitability. This helps identify the most valuable customer group.

**Question:**  
Which customer segments generate the highest sales and profit?

**SQL Query:**
```sql
SELECT 
    Segment,
    SUM(Sales) AS total_sales,
    SUM(Profit) AS total_profit
FROM Superstore
GROUP BY Segment
ORDER BY total_profit DESC;
```

