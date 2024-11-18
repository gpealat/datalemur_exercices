## Problem
Your team at JPMorgan Chase is preparing to launch a new credit card, and to gain some insights, you're analyzing how many credit cards were issued each month.

Write a query that outputs the name of each credit card and the difference in the number of issued cards between the month with the highest issuance cards and the lowest issuance. Arrange the results based on the largest disparity.

## Solution

    SELECT data.card as card_name, max(data.s) - min(data.s) AS difference
    FROM 
      (SELECT card_name AS card, sum(issued_amount) AS s FROM monthly_cards_issued
      GROUP BY card_name, issue_month) AS data
    GROUP BY data.card
    ORDER BY difference DESC
