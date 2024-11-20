## Problem

Assume you are given the table below on Uber transactions made by users. Write a query to obtain the third transaction of every user. Output the user id, spend and transaction date.

## Solution

    WITH RANK AS (
    SELECT
      user_id, spend, transaction_date,
      DENSE_RANK() OVER(PARTITION BY user_id ORDER BY transaction_date) AS rank
    FROM
      transactions
    )

    SELECT
      RANK.user_id, RANK.spend, RANK.transaction_date
    FROM RANK
    WHERE 
      RANK.rank = 3
  
