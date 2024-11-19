## Problem

Assume you have an events table on Facebook app analytics. Write a query to calculate the click-through rate (CTR) for the app in 2022 and round the results to 2 decimal places.

Definition and note:

Percentage of click-through rate (CTR) = 100.0 * Number of clicks / Number of impressions
To avoid integer division, multiply the CTR by 100.0, not 100.

## Solution

    SELECT clicks.app_id, ROUND(CAST(100 * clicks.c / impressions.c AS NUMERIC),2)
    FROM
    (
      SELECT app_id, event_type, CAST(count(event_type) AS FLOAT) AS c
      FROM events
      WHERE EXTRACT(YEAR FROM timestamp) = 2022
      AND event_type = 'click'
      GROUP BY app_id, event_type
      ) AS clicks,
    (
      SELECT app_id, event_type, CAST(count(event_type) AS FLOAT) AS c
      FROM events
      WHERE EXTRACT(YEAR FROM timestamp) = 2022
      AND event_type = 'impression'
      GROUP BY app_id, event_type
      ) AS impressions
    GROUP BY clicks.app_id, clicks.c, impressions.c
