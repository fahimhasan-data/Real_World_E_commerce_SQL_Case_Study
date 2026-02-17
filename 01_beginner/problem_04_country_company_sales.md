# Problem 04: Countries Where the Company Generates Sales

---

## 1. Business Objective

Identify the countries where the company has successfully generated revenue through completed transactions.

This helps the business:

- Understand geographic market reach
- Evaluate international expansion
- Identify high-potential regions
- Support regional performance analysis

---

## 2. Business Context

The dataset contains transaction records, including cancellations and potentially invalid entries.

If we list countries without filtering:

- Markets with only cancelled transactions may appear as active
- Geographic presence may be overstated
- Strategic decisions may rely on inaccurate data

Therefore, we must define what qualifies as a valid sale.

---

## 3. Definition of a Valid Sale

For this analysis, a valid sale must:

- Not be a cancelled invoice (InvoiceNo NOT starting with 'C')
- Have quantity greater than 0
- Have unit price greater than 0

Only countries associated with valid sales will be considered active markets.

---

## 4. Analytical Strategy

Step 1: Filter out cancelled transactions  
Step 2: Remove invalid quantity and price records  
Step 3: Extract unique country values  

---

## 5. SQL Implementation

```sql
SELECT 
    country,
    SUM(quantity) AS total_quantity_sold
FROM online_retail
WHERE invoice_no NOT LIKE 'C%'
  AND quantity > 0
  AND unit_price > 0
GROUP BY country
ORDER BY total_quantity_sold DESC;
