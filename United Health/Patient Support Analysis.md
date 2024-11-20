## Problem

UnitedHealth Group (UHG) has a program called Advocate4Me, which allows policy holders (or, members) to call an advocate and receive support for their health care needs – whether that's claims and benefits support, drug coverage, pre- and post-authorisation, medical records, emergency assistance, or member portal services.

Write a query to find how many UHG policy holders made three, or more calls, assuming each call is identified by the case_id column.

## Solution

    SELECT COUNT(policy_holder_id)
    FROM
      (
      SELECT policy_holder_id, COUNT(case_id) AS num
      FROM callers
      GROUP BY policy_holder_id
      ORDER BY num DESC
      ) AS t
    WHERE t.num >=3