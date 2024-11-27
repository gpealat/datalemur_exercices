## Problem

As part of an ongoing analysis of salary distribution within the company, your manager has requested a report identifying high earners in each department. 
A 'high earner' within a department is defined as an employee with a salary ranking among the top three salaries within that department.

You're tasked with identifying these high earners across all departments. Write a query to display the employee's name along with their department name and salary. 
In case of duplicates, sort the results of department name in ascending order, then by salary in descending order. If multiple employees have the same salary, then order them alphabetically.

Note: Ensure to utilize the appropriate ranking window function to handle duplicate salaries effectively.

## Solution
```
SELECT department_name, name, salary
FROM
(
  SELECT D.department_name, E.name, E.salary, DENSE_RANK() OVER (PARTITION BY D.department_name ORDER BY E.salary DESC)
  FROM 
    employee AS E,
    department AS D
  WHERE
    E.department_id = D.department_id
  ) AS A
  WHERE A.dense_rank < 4
```
