# Top 10 Products by Total Revenue

## 1. Business Objective

Identify the top 10 revenue-generating products to support:

- Inventory prioritization
- Marketing focus
- Supplier negotiation strategy
- Revenue concentration analysis

---

## 2. KPI Definition

Revenue per product = SUM(quantity × unit_price)

Only valid transactions considered:

- Exclude cancelled invoices (invoice_no NOT LIKE 'C%')
- quantity > 0
- unit_price > 0

---

## 3. Business Risk

Incorrect revenue calculation can:

- Inflate product performance
- Mislead marketing allocation
- Distort inventory decisions
- Create revenue concentration blind spots

Data validation ensures strategic accuracy.

---

## 4. SQL Query

WITH valid_sales AS (
    SELECT *
    FROM online_retail
    WHERE invoice_no NOT LIKE 'C%'
      AND quantity > 0
      AND unit_price > 0
)

SELECT
    description,
    ROUND(SUM(quantity * unit_price), 2) AS total_revenue
FROM valid_sales
GROUP BY description
ORDER BY total_revenue DESC
LIMIT 10;

---

## 5. Interpretation

The result shows the top 10 products generating the highest total revenue.

This helps identify revenue-driving SKUs and potential over-reliance on specific products.

---

## 6. Business Decisions

If revenue is highly concentrated:
- Reduce dependency risk by diversifying product promotions
- Develop similar high-margin products

For top-performing products:
- Ensure strong inventory management
- Negotiate better supplier terms
- Bundle with slow-moving inventory

For lower-ranked products:
- Consider discount strategies
- Reposition or discontinue if necessary

---

## 7. Analyst Skills Demonstrated

- KPI framing before SQL
- Data validation logic
- Revenue aggregation
- Ranking logic
- Strategic recommendation alignment
