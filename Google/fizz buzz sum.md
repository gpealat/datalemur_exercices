## Problem
Write a function fizz_buzz_sum to find the sum of all multiples of 3 or 5 below a target value.

## Solution

    def fizz_buzz_sum(target):
      res =[]
  
      for i in range(1, target):
        if (i%3) == 0:
          res.append(i)
        elif (i%5) == 0:
          res.append(i)
  
      return sum(res)
