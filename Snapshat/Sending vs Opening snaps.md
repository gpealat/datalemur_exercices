## Problem

Assume you're given tables with information on Snapchat users, including their ages and time spent sending and opening snaps.

Write a query to obtain a breakdown of the time spent sending vs. opening snaps as a percentage of total time spent on these activities grouped by age group. Round the percentage to 2 decimal places in the output.

Notes:

Calculate the following percentages:
time spent sending / (Time spent sending + Time spent opening)
Time spent opening / (Time spent sending + Time spent opening)
To avoid integer division in percentages, multiply by 100.0 and not 100.

## Solution

    SELECT
    age.age_bucket,
    ROUND( 100.0 * stats.send_perc / (stats.send_perc + stats.open_perc),2) AS send_perc,
    ROUND( 100.0 * stats.open_perc / (stats.send_perc + stats.open_perc),2) AS open_perc
    FROM
    age_breakdown as age,
    (
      SELECT
      user_id,
      SUM(time_spent) FILTER (WHERE activity_type = 'send') as send_perc,
      SUM(time_spent) FILTER (WHERE activity_type = 'open') as open_perc
      FROM
      activities
      WHERE
      activity_type IN ('send','open')
      GROUP BY user_id
      ) AS stats
    WHERE
    age.user_id = stats.user_id
    ORDER BY age.age_bucket
