## Problem

Assume you're given the tables containing completed trade orders and user details in a Robinhood trading system.

Write a query to retrieve the top three cities that have the highest number of completed trade orders listed in descending order. Output the city name and the corresponding number of completed trade orders.

## Solution

    SELECT A.city, SUM(A.C) AS total_orders
    FROM
    (
      SELECT 
      u.city, COUNT(t.user_id) AS C
      FROM
      trades AS t,
      users AS u
      WHERE
      t.status = 'Completed'
      AND 
      t.user_id = u.user_id
      GROUP BY u.city, u.user_id
    ) AS A
    GROUP BY A.city
    ORDER BY SUM(A.C) DESC
    LIMIT 3
