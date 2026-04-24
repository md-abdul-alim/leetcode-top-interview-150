# Description
Given an integer array nums, return true if any value appears more than once in the array, otherwise return false.

---
## 1. Brute Force
### Intuition
We can check every pair of different elements in the array and return true if any pair has equal values.
This is the most intuitive approach because it directly compares all possible pairs, but it is also the least efficient since it examines every combination.

### Algorithm
Iterate through the array using two nested loops to check all possible pairs of distinct indices.
If any pair of elements has the same value, return true.
If all pairs are checked and no duplicates are found, return false.

```python
nums = [1, 2, 3, 3]

def hasDuplicate(nums) -> bool:
    for i in range(len(nums)):
        for j in range(i+1, len(nums)):
            if nums[i] == nums[j]:
                return True
    return False
```

### Time & Space Complexity
- Time complexity: O ( n 2 )
- Space complexity: O(1)
---
