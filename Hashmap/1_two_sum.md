# Description
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

 

Example 1:
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```
Example 2:
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```
## 1. Brute Force
### Intuition
We can check every pair of different elements in the array and return the first pair that sums up to the target. This is the most intuitive approach but it's not the most efficient.

### Algorithm
Iterate through the array with two nested loops using indices i and j to check every pair of different elements.
If the sum of the pair equals the target, return the indices of the pair.
If no such pair is found, return an empty array.
There is guaranteed to be exactly one solution, so we will never return an empty array.

```python
nums = [2, 7, 11, 15]
target = 9

def twoSum(nums) -> List[int]:
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[j] + nums[i] == target:
                return [i, j]
        
    return []

```

### Time & Space Complexity
- Time complexity: O (n^2)
- Space complexity: O(1)

---

