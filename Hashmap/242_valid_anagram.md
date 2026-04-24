# Description
Given two strings s and t, return true if the two strings are anagrams of each other, otherwise return false.

An anagram is a string that contains the exact same characters as another string, but the order of the characters can be different.

Example 1:

```
Input: s = "racecar", t = "carrace"
Output: true
```

Example 2:
```
Input: s = "jar", t = "jam"
Output: false
```

# 1. Sorting

## Intuition
If two strings are anagrams, they must contain exactly the same characters with the same frequencies.
By sorting both strings, all characters will be arranged in a consistent order.
If the two sorted strings are identical, then every character and its count match, which means the strings are anagrams.

## Algorithm
1. If the lengths of the two strings differ, return false immediately because they cannot be anagrams.
2. Sort both strings.
3. Compare the sorted versions of the strings:
- If they are equal, return true.
- Otherwise, return false.

```python
s = "anagram"
t = "nagaram"

def isAnagram(s, t) -> bool:
    if len(s) !=len(t):
        return False
    return sorted(s) == sorted(t)
```

### Time & Space Complexity
- Time complexity: O(nlogn + mlogm)
- Space complexity: O(1)
---
