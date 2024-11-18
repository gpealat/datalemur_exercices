## Problem
Companies often perform salary analyses to ensure fair compensation practices. One useful analysis is to check if there are any employees earning more than their direct managers.

As a HR Analyst, you're asked to identify all employees who earn more than their direct managers. The result should include the employee's ID and name.

## Solution

    SELECT employees.employee_id, employees.name  FROM 
      (SELECT employee_id, salary, name FROM employee 
      WHERE manager_id IS NULL) AS manager,
      (SELECT employee_id, salary, manager_id, name FROM employee 
      WHERE manager_id IS NOT NULL) AS employees
    WHERE
    employees.manager_id = manager.employee_id
    AND employees.salary >= manager.salary;
