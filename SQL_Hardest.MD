Hardest: Real interview-style SQL

1. Compare first order vs latest order

Question: Which customers have a latest order amount higher than their first order amount?

WITH ranked_orders AS (
    SELECT
        o.*,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date
        ) AS first_order_rank,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date DESC
        ) AS latest_order_rank
    FROM orders o
    WHERE status = 'Completed'
),
first_orders AS (
    SELECT
        customer_id,
        order_id AS first_order_id,
        order_date AS first_order_date,
        total_amount AS first_order_amount
    FROM ranked_orders
    WHERE first_order_rank = 1
),
latest_orders AS (
    SELECT
        customer_id,
        order_id AS latest_order_id,
        order_date AS latest_order_date,
        total_amount AS latest_order_amount
    FROM ranked_orders
    WHERE latest_order_rank = 1
)
SELECT
    c.customer_name,
    f.first_order_id,
    f.first_order_date,
    f.first_order_amount,
    l.latest_order_id,
    l.latest_order_date,
    l.latest_order_amount,
    l.latest_order_amount - f.first_order_amount AS amount_difference
FROM first_orders f
JOIN latest_orders l
    ON f.customer_id = l.customer_id
JOIN customers c
    ON f.customer_id = c.customer_id
WHERE l.latest_order_amount > f.first_order_amount
ORDER BY amount_difference DESC;

2. Top-selling product in each category
WITH product_sales AS (
    SELECT
        p.category,
        p.product_name,
        SUM(oi.quantity) AS units_sold,
        SUM(oi.quantity * oi.unit_price) AS revenue,
        RANK() OVER (
            PARTITION BY p.category
            ORDER BY SUM(oi.quantity * oi.unit_price) DESC
        ) AS category_rank
    FROM order_items oi
    JOIN orders o
        ON oi.order_id = o.order_id
    JOIN products p
        ON oi.product_id = p.product_id
    WHERE o.status = 'Completed'
    GROUP BY 
        p.category,
        p.product_name
)
SELECT
    category,
    product_name,
    units_sold,
    revenue
FROM product_sales
WHERE category_rank = 1
ORDER BY revenue DESC;

3. Customer’s favorite category by spending
WITH category_spending AS (
    SELECT
        c.customer_id,
        c.customer_name,
        p.category,
        SUM(oi.quantity * oi.unit_price) AS category_spend
    FROM customers c
    JOIN orders o
        ON c.customer_id = o.customer_id
    JOIN order_items oi
        ON o.order_id = oi.order_id
    JOIN products p
        ON oi.product_id = p.product_id
    WHERE o.status = 'Completed'
    GROUP BY 
        c.customer_id,
        c.customer_name,
        p.category
),
ranked_categories AS (
    SELECT
        *,
        RANK() OVER (
            PARTITION BY customer_id
            ORDER BY category_spend DESC
        ) AS category_rank
    FROM category_spending
)
SELECT
    customer_id,
    customer_name,
    category,
    category_spend
FROM ranked_categories
WHERE category_rank = 1
ORDER BY category_spend DESC;
