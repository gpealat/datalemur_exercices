## Problem
Tesla is investigating production bottlenecks and they need your help to extract the relevant data. Write a query to determine which parts have begun the assembly process but are not yet finished.

## Solution

    SELECT part, assembly_step FROM parts_assembly 
    WHERE finish_date IS NULL;
