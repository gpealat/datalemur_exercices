## Problem
Write a function to get the intersection of two lists.

## Solution

    def intersection(a, b):
      inter = []
  
      for i in a:
        if i in b:
          inter.append(i)
      
      return inter
  
