# Problem 03: Unique Order Count (Validated Order KPI)

---

## 1. Business Objective

Determine the total number of unique valid orders placed by customers.

Order count is a core operational KPI used to:

- Measure transaction volume
- Track demand patterns
- Evaluate business growth
- Support conversion analysis

---

## 2. Business Context

The dataset includes cancelled transactions and invalid entries. 

If we count all invoices without validation:

- Order volume may be overstated
- Growth trends may be misleading
- Operational planning may be inaccurate

Therefore, we define and compute a validated order count.

---

## 3. Order Definition

For this analysis, a valid order is defined as:

- An invoice not marked as cancelled (InvoiceNo NOT starting with 'C')
- Quantity greater than 0
- Unit price greater than 0

Each invoice number represents one unique order.

---

## 4. Data Validation Rules

- Exclude cancelled invoices
- Exclude negative or zero quantities
- Exclude zero or negative prices

This ensures we count only completed revenue-generating orders.

---

## 5. Analytical Strategy

Step 1: Filter valid transactions  
Step 2: Identify distinct invoice numbers  
Step 3: Count unique invoices  

---

## 6. SQL Implementation

```sql
SELECT 
    COUNT(DISTINCT invoice_no) AS total_orders
FROM online_retail
WHERE invoice_no NOT LIKE 'C%'
  AND quantity > 0
  AND unit_price > 0;
