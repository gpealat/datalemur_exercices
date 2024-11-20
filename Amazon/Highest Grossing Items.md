## Problem

Assume you're given a table containing data on Amazon customers and their spending on products in different category, write a query to identify the top two highest-grossing products within each category in the year 2022. 
The output should include the category, product, and total spend.

## Solution

    SELECT
    category, product, sum as total_spend
    FROM
    (
      SELECT 
      category, product, SUM(spend), 
      DENSE_RANK() OVER( PARTITION BY category ORDER BY SUM(spend) DESC)
      FROM product_spend
      WHERE
      EXTRACT(YEAR FROM transaction_date) = 2022
      GROUP BY category, product
    ) AS a
    WHERE
    dense_rank <=2
