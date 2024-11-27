## Problem

Assume you're given tables with information about TikTok user sign-ups and confirmations through email and text. 
New users on TikTok sign up using their email addresses, and upon sign-up, each user receives a text message confirmation to activate their account.

Write a query to display the user IDs of those who did not confirm their sign-up on the first day, but confirmed on the second day.

## Solution
```
SELECT user_id
FROM 
  (
  SELECT A.user_id, B.action_date - A.signup_date AS NUMERIC
  FROM 
    emails AS A,
    texts AS B
  WHERE
    A.email_id = B.email_id
    AND
    B.signup_action = 'Confirmed'
    AND
    A.signup_date  != B.action_date
    ) AS C
WHERE
  DATE_PART('day', numeric) = 1
```
