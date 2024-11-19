## Problem

Assume you're given a table containing job postings from various companies on the LinkedIn platform. Write a query to retrieve the count of companies that have posted duplicate job listings.

*Definition*:

Duplicate job listings are defined as two job listings within the same company that share identical titles and descriptions.

## Solution

     SELECT COUNT(A.duplicate_companies) AS duplicate_companies FROM
     (
       SELECT COUNT(company_id) AS duplicate_companies FROM job_listings
       GROUP BY company_id, title, description
       HAVING COUNT(description) > 1
      ) AS A
