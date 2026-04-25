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

## 2. Sorting
### Intuition
We can sort the array and use two pointers to find the two numbers that sum up to the target. This is more efficient than the brute force approach. This approach is similar to the one used in Two Sum II.

### Algorithm
1. Create a copy of the array and sort it in ascending order.
2. Initialize two pointers, one at the beginning (i) and one at the end (j) of the array.
3. Iterate through the array with the two pointers and check if the sum of the two numbers is equal to the target.
4. If the sum is equal to the target, return the indices of the two numbers.
5. If the sum is less than the target, move the left pointer i to the right, which will increase the sum.
6. If the sum is greater than the target, move the right pointer j to the left, which will decrease the sum.
7. There is guaranteed to be exactly one solution, so we will never return an empty array.

```python
nums = [2, 7, 11, 15]
target = 9

def twoSum(nums):
    A = []
    for i, num in enumerate(nums):
        A.append([num, i])

    A.sort()
    i, j = 0, len(nums) - 1

    while i < j:
        current = A[i][0] + A[j][0]
        if current == target:
            return [min(A[i][1], A[j][1]), max(A[i][1], A[j][1])]
        elif current < target:
            i += 1
        else:
            j -=1
    return []
```
---

### Time & Space Complexity
- Time complexity: O (nlogn)
- Space complexity: O(n)
---

## 3. Hash Map (Two Pass)
### Intuition
We can use a hash map to store the value and index of each element in the array. Then, we can iterate through the array and check if the complement of the current element exists in the hash map. The complement must be at a different index, because we can't use the same element twice.

By using a hashmap, we can achieve a time complexity of O(n) because the insertion and lookup time of a hashmap is O(1).

### Algorithm
1. Create a hash map to store the value and index of each element in the array.
2. Iterate through the array and compute the complement of the current element, which is target - nums[i].
3. Check if the complement exists in the hash map.
4. If it does, return the indices of the current element and its complement.
5. If no such pair is found, return an empty array.

```python
nums = [2, 7, 11, 15]
target = 9

def twoSum(nums):
    indices = {} # val -> index

    for i, n in enumerate(nums):
        indices[n] = i

    for i, n in enumerate(nums):
        diff = target - n

        if diff in indices and indices[diff] != i:
            return [i, indices[diff]]

    return []
```
---
### Time & Space Complexity
- Time complexity: O(n)
- Space complexity: O(n)
---

## 4. Hash Map (One Pass)
### Intuition
We can solve the problem in a single pass by iterating through the array and checking if the complement of the current element exists in the hash map.

If it does, we return the indices of the current element and its complement. If not, we store the current element in the hash map. This guarantees that we will never use the same element twice, but we still check every element in the array.

### Algorithm
1. Create a hash map to store the value and index of each element in the array.
2. Iterate through the array using index i and compute the complement of the current element, which is target - nums[i].
3. Check if the complement exists in the hash map.
4. If it does, return the indices of the current element and its complement.
5. If no such pair is found, return an empty array.

```python
nums = [2, 7, 11, 15]
target = 9

def twoSum(nums):
    prevMap = {}

    for i, n in enumerate(nums):
        diff = target - n
        if diff in prevMap:
            return [prevmap[diff], i]
        prevMap[n] = i
```
---
### Time & Space Complexity
- Time complexity: O(n)
- Space complexity: O(n)
---