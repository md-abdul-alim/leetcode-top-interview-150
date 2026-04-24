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
## 2. Sorting
### Intuition
If we sort the array, then any duplicate values will appear next to each other.
Sorting groups identical elements together, so we can simply check adjacent positions to detect duplicates.
This reduces the problem to a single linear scan after sorting, making it easy to identify if any value repeats.

### Algorithm
Sort the array in non-decreasing order.
Iterate through the array starting from index 1.
Compare the current element with the previous element.
If both elements are equal, we have found a duplicate — return true.
If the loop finishes without detecting equal neighbors, return false.

```python
nums = [1, 2, 3, 4]

def hasDuplicate(nums):
    nums.sort()
    for i in range(1, len(nums)):
        if nums[i] == nums[i - 1]:
            return True
    return False
```
### Time & Space Complexity
- Time complexity: O ( n log n )
- Space complexity: O(1) or O(n) depending on the sorting algorithm.
---
## Hash Set

### Intuition
We can use a hash set to efficiently keep track of the values we have already encountered.
As we iterate through the array, we check whether the current value is already present in the set.
If it is, that means we've seen this value before, so a duplicate exists.
Using a hash set allows constant-time lookups, making this approach much more efficient than comparing every pair.

### Algorithm
Initialize an empty hash set to store seen values.
Iterate through each number in the array.
For each number:
If it is already in the set, return true because a duplicate has been found.
Otherwise, add it to the set.
If the loop finishes without finding any duplicates, return false.

```python
nums = [1, 2, 3, 4, 5]

def hasDuplicate(nums):
    seen = set()

    for num in nums:
        if num in seen:
            return True
        seen.add(num)
    return False
```

### Time & Space Complexity
- Time complexity: O (n)
- Space complexity: O(n)
---

