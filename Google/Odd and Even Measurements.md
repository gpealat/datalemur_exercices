## Problem

Assume you're given a table with measurement values obtained from a Google sensor over multiple days with measurements taken multiple times within each day.

Write a query to calculate the sum of odd-numbered and even-numbered measurements separately for a particular day and display the results in two different columns. Refer to the Example Output below for the desired format.

Definition:

Within a day, measurements taken at 1st, 3rd, and 5th times are considered odd-numbered measurements, and measurements taken at 2nd, 4th, and 6th times are considered even-numbered measurements.

## Solution

    WITH A AS(
    SELECT 
      CAST(measurement_time AS DATE) AS formatted_date,
      measurement_time, measurement_id, measurement_value
    FROM measurements
    ),
    B AS (
    SELECT
      formatted_date,
      DENSE_RANK() OVER(PARTITION BY formatted_date ORDER BY measurement_time ASC),
      measurement_time, measurement_id, measurement_value
      FROM A
    )

    SELECT 
      formatted_date as measurement_day,
      SUM(measurement_value) FILTER (WHERE dense_rank%2 != 0) as odd_sum,
      SUM(measurement_value) FILTER (WHERE dense_rank%2 = 0) as even_sum
  
    FROM B
    GROUP BY formatted_date
