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

# 2. Hash Map
## Intuition
If two strings are anagrams, they must use the same characters with the same frequencies.
Instead of sorting, we can count how many times each character appears in both strings.
By using two hash maps (or dictionaries), we track the frequency of every character in each string.
If both frequency maps match exactly, then the strings contain the same characters with same frequencies, meaning they are anagrams.

## Algorithm
1. If the two strings have different lengths, return false immediately.
2. Create two hash maps to store character frequencies for each string.
3 Iterate through both strings at the same time:
- Increase the character count for s[i] in the first map.
- Increase the character count for t[i] in the second map.
4. After building both maps, compare them:
- If the maps are equal, return true.
- Otherwise, return false.

```python
s = "anagram"
t = "nagaram"

def isAnagram(s, t) -> bool:
    if len(s) !=len(t):
        return False

    countS, countT = {}, {}

    for i in range(len(s)):
        countS[s[i]] = 1 + countS.get(s[i], 0)
        countT[t[i]] = 1 + countT.get(t[i], 0)

    for c in countS:
        if countS[c] != countT.get(c, 0):
            return False
    
    return True

```

### Time & Space Complexity
- Time complexity: O(n + m)
- Space complexity: O(1) since we have at most 26 different characters.
---