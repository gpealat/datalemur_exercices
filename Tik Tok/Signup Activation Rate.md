## Problem

New TikTok users sign up with their emails. They confirmed their signup by replying to the text confirmation to activate their accounts. Users may receive multiple text messages for account confirmation until they have confirmed their new account.

A senior analyst is interested to know the activation rate of specified users in the emails table. Write a query to find the activation rate. Round the percentage to 2 decimal places.

Definitions:

emails table contain the information of user signup details.
texts table contains the users' activation information.
Assumptions:

The analyst is interested in the activation rate of specific users in the emails table, which may not include all users that could potentially be found in the texts table.
For example, user 123 in the emails table may not be in the texts table and vice versa.

## Solution

    SELECT
    ROUND(ROUND(100.0 * conf / (conf + pend), 0) /100.0,2) as confirm_rate
    FROM
    (
      SELECT 
        COUNT(signup_action) FILTER (WHERE signup_action = 'Confirmed') AS conf,
        COUNT(signup_action) FILTER (WHERE signup_action = 'Not Confirmed') AS pend
      FROM 
        emails AS E,
        texts AS T
      WHERE
        E.email_id = T.email_id
      ) AS A
  
