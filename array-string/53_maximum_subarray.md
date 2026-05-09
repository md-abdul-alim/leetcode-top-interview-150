---
title: Maximum Subarray
---

# Maximum Subarray

<DifficultyBadge level="medium" />

## Description

[Problem Link](https://leetcode.com/problems/maximum-subarray/)

Given an integer array `nums`, find the contiguous subarray with the highest total and return that total.

A subarray must contain at least one element.

### Examples

```txt
Input: nums = [-1,4,-2,5,-7,3]
Output: 7
```
Explanation: The subarray `[4,-2,5]` gives the maximum sum `7`.

<SubarrayBarsFigure
  values={[-1, 4, -2, 5, -7, 3]}
  highlightIndices={[1, 2, 3]}
  ariaLabel="Maximum subarray visual for first example"
  className="pt-6"
/>

---

```txt
Input: nums = [-5,-2,-9]
Output: -2
```
Explanation: When all values are negative, the best subarray is the single value `[-2]`.

---

```txt
Input: nums = [3,-1,2,-1,4,-5,2]
Output: 7
```
Explanation: The subarray `[3,-1,2,-1,4]` has sum `7`, which is the largest possible.

### Constraints

- `1 <= nums.length <= 10⁵`
- `-10⁴ <= nums[i] <= 10⁴`
- `nums[i]` is an integer.

## Solution

### Idea

Use Kadane's algorithm with one pass.

Keep two values while scanning:
- `cur_sum`: best sum of a subarray that must end at the current index
- `max_sum`: best subarray sum seen anywhere so far

At each number:
- Either start fresh from this number
- Or extend the previous subarray

So we set `cur_sum = max(num, cur_sum + num)` and update `max_sum`.

This is required because `cur_sum` means "best subarray sum that must end at this index".
If the previous `cur_sum` is negative, extending it makes things worse, so we restart at `num`.
If it is positive, extending helps, so `cur_sum + num` is better.

### Code

```python filename="Python 3"
from typing import List

class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        cur_sum = nums[0]
        max_sum = nums[0]

        for num in nums[1:]:
            cur_sum = max(num, cur_sum + num)
            max_sum = max(max_sum, cur_sum)

        return max_sum
```

> **Note:** Avoid `cur_sum, max_sum = 0, 0`. That fails on all-negative arrays (for example `[-3, -1, -2]`) by incorrectly returning `0`. If you prefer `for num in nums`, use `cur_sum = 0` and `max_sum = nums[0]`.

### Complexity

- Time: `O(n)`. We visit each element once.
- Space: `O(1)`. We only keep two running values.

### Logs

```ansi
Input: nums = [3,-1,2,-1,4,-5,2]

[init] cur_sum=3 max_sum=3

[1] num=-1
    cur_sum=max(-1,3+(-1))=2
    max_sum=max(3,2)=3

[2] num=2
    cur_sum=max(2,2+2)=4
    max_sum=max(3,4)=4

[3] num=-1
    cur_sum=max(-1,4+(-1))=3
    max_sum=max(4,3)=4

[4] num=4
    cur_sum=max(4,3+4)=7
    max_sum=max(4,7)=7

[5] num=-5
    cur_sum=max(-5,7+(-5))=2
    max_sum=max(7,2)=7

[6] num=2
    cur_sum=max(2,2+2)=4
    max_sum=max(7,4)=7

Output: 7
```