# Description
Given an array of strings strs, group all anagrams together into sublists. You may return the output in any order.

An anagram is a string that contains the exact same characters as another string, but the order of the characters can be different.https://www.youtube.com/watch?v=GX7Tbh1fQfI

Example 1:

Input: strs = ["act","pots","tops","cat","stop","hat"]

Output: [["hat"],["act", "cat"],["stop", "pots", "tops"]]

## 2. Hash Table
### Intuition
Instead of sorting each string, we can represent every string by the frequency of its characters.
Since the problem uses lowercase English letters, a fixed-size array of length 26 can capture how many times each character appears.
Two strings are anagrams if and only if their frequency arrays are identical.
By using this frequency array (converted to a tuple so it can be a dictionary key), we can group all strings that share the same character counts.

### Algorithm
1. Create a hash map where each key is a 26-length tuple representing character frequencies, and each value is a list of strings belonging to that anagram group.
2. For each string in the input:
    - Initialize a count array of size 26 with all zeros.
    - For each character c in the string, increment the count at the corresponding index.
    - Convert the count array to a tuple and use it as the key.
    - Append the string to the list associated with this key.
3. After processing all strings, return all the lists stored in the hash map.

---
```python
def groupAnagrams(strs):
    res = defaultdict(list)

    for s in strs:
        count = [0] * 26
        for letter in s:
            count[ord(letter) - ord('a')] += 1 # count index is replacing by string ANSI number
        res[tuple(count)] = s
    
    return list(res.values())
```

### Time & Space Complexity
- Time complexity: O(m * n)
- Space complexity: 
    - O(m) extra space
    - O(m*n) space for the output list
::: Where m is the number of the strings and n is the length of the longest string
---
