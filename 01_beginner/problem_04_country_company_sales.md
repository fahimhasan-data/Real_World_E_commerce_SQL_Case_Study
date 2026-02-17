# Problem 05: Revenue Contribution by Country (Market Concentration Analysis)

---

## 1. Business Objective

Determine how much revenue each country contributes as a percentage of total company revenue.

This helps the business:

- Identify primary revenue-driving markets
- Measure geographic concentration risk
- Evaluate diversification opportunities
- Support international expansion strategy

---

## 2. Business Context

Knowing where the company sells is useful.

However, knowing **how much each country contributes financially** is far more strategic.

If revenue is heavily concentrated in one region:

- The business becomes vulnerable to local economic shifts
- Regulatory or market disruptions can severely impact performance
- Diversification strategy becomes critical

Therefore, we calculate revenue contribution percentage by country.

---

## 3. Revenue Definition

Revenue = Quantity × Unit Price

Only valid completed transactions are included:

- Exclude cancelled invoices (InvoiceNo NOT starting with 'C')
- Exclude Quantity ≤ 0
- Exclude Unit Price ≤ 0

---

## 4. Analytical Strategy

Step 1: Filter valid transactions  
Step 2: Calculate revenue per country  
Step 3: Compute total company revenue  
Step 4: Calculate percentage contribution per country  
Step 5: Rank countries by contribution  

---

## 5. SQL Implementation

```sql
SELECT 
    country,
    ROUND(SUM(quantity * unit_price), 2) AS total_revenue,
    ROUND(
        SUM(quantity * unit_price) * 100.0 
        / SUM(SUM(quantity * unit_price)) OVER (), 
        4
    ) AS revenue_percentage
FROM online_retail
WHERE invoice_no NOT LIKE 'C%'
  AND quantity > 0
  AND unit_price > 0
GROUP BY country
ORDER BY revenue_percentage DESC;
