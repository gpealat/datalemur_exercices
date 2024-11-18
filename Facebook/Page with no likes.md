## Problem

Assume you're given two tables containing data about Facebook Pages and their respective likes (as in "Like a Facebook Page").
Write a query to return the IDs of the Facebook pages that have zero likes. The output should be sorted in ascending order based on the page IDs.

## Solution

    SELECT candidate_id FROM candidates
    WHERE skill IN ('Python', 'PostgreSQL','Tableau')
    GROUP BY candidate_id
    HAVING COUNT(candidate_id) = 3
    ORDER BY candidate_id
