# Problem 02: Unique Customer Count (Validated Customer Base KPI)

---

## 1. Business Objective

Determine the total number of unique customers who have completed at least one valid transaction.

Customer count is a critical KPI used to:

- Measure business reach
- Evaluate customer acquisition performance
- Support growth analysis
- Estimate customer lifetime value potential

---

## 2. Business Context

The dataset includes transactional records with cancellations and possible missing customer IDs.

If we count customers without validation:

- Customer base may be overstated
- Growth metrics may be misleading
- Marketing efficiency may be miscalculated

Therefore, we must define and calculate a **validated active customer count**.

---

## 3. Customer Definition

For this analysis:

A valid customer is defined as:
- A customer with at least one completed transaction
- Associated with a non-cancelled invoice
- Having a non-null customer_id

---

## 4. Data Validation & Assumptions

To ensure accuracy, we apply the following filters:

- Exclude cancelled invoices (InvoiceNo starting with 'C')
- Exclude negative or zero quantities
- Exclude zero or negative unit prices
- Exclude NULL customer_id values

This ensures we count only customers who generated real revenue.

---

## 5. Analytical Strategy

Step 1: Filter valid transactions  
Step 2: Identify distinct customer IDs  
Step 3: Count unique customers  

This ensures the metric reflects actual paying customers.

---

## 6. SQL Implementation

```sql
SELECT 
    COUNT(DISTINCT customer_id) AS unique_customers
FROM online_retail
WHERE invoice_no NOT LIKE 'C%'
  AND quantity > 0
  AND unit_price > 0
  AND customer_id IS NOT NULL;
