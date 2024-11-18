## Problem
Given an list of integers called input, return True if any value appears at least twice in the array. Return False if every element in the input list is distinct.

## Solution

    def contains_duplicate(input)-> bool:
  
      for i in range(len(input)):
        if i in input[i+1:]:
          return True
      
      return False
