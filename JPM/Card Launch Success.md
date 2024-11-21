## Problem

Your team at JPMorgan Chase is soon launching a new credit card. You are asked to estimate how many cards you'll issue in the first month.

Before you can answer this question, you want to first get some perspective on how well new credit card launches typically do in their first month.

Write a query that outputs the name of the credit card, and how many cards were issued in its launch month. 
The launch month is the earliest record in the monthly_cards_issued table for a given card. 
Order the results starting from the biggest issued amount.

## Solution

    WITH A AS(
    SELECT card_name, 
            DENSE_RANK() OVER( PARTITION BY card_name ORDER BY issue_year, issue_month), issued_amount
    FROM monthly_cards_issued
    )

    SELECT 
      card_name,
      SUM(issued_amount) FILTER(WHERE dense_rank = 1) AS issued_amount
    FROM A
    GROUP BY card_name
    ORDER BY issued_amount DESC
