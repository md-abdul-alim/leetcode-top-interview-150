---
title: Product of Array Except Self
---

# Product of Array Except Self

<DifficultyBadge level="medium" />

## Description

[Problem Link](https://leetcode.com/problems/product-of-array-except-self/)

Given an integer array `nums`, build an array `ans` where each `ans[i]` is the product of every value in `nums` except `nums[i]`.

You must solve it in linear time and without using division.

### Examples

```txt
Input: nums = [2,3,4,5]
Output: [60,40,30,24]
```
Explanation: `60 = 3 * 4 * 5`, `40 = 2 * 4 * 5`, `30 = 2 * 3 * 5`, `24 = 2 * 3 * 4`.

---

```txt
Input: nums = [1,0,7,2]
Output: [0,14,0,0]
```
Explanation: Only index `1` skips the zero, so that position gets `1 * 7 * 2 = 14`.

---

```txt
Input: nums = [-2,3,-4]
Output: [-12,8,-6]
```
Explanation: `-12 = 3 * (-4)`, `8 = (-2) * (-4)`, `-6 = (-2) * 3`.

### Constraints

- `2 <= nums.length <= 10⁵`
- `-30 <= nums[i] <= 30`
- The product of any prefix or suffix of `nums` fits in a 32-bit integer.
- Do not use division.

## Solution

### Idea

For each index, we need:
- Product of all numbers to its left.
- Product of all numbers to its right.

We can do this in two passes:
1. Left-to-right: store left products in `ans`.
2. Right-to-left: keep a running right product and multiply into `ans`.

This avoids division and uses only constant extra space (not counting output).

### Code

```python filename="Python 3"
from typing import List

class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        ans = [1] * n

        left = 1
        for i in range(n):
            ans[i] = left
            left *= nums[i]

        right = 1
        for i in range(n - 1, -1, -1):
            ans[i] *= right
            right *= nums[i]

        return ans
```

### Time and space Complexity

- Time: `O(n)`. We scan the array twice.
- Space: `O(1)`. Extra space is constant (output array is not counted).
