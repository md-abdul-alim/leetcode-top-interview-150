!!!Important 
# Description
https://neetcode.io/solutions/top-k-frequent-elements

## 1. Sorting

```python

def topKFrequent(nums, k):
    count = {}
    for num in nums:
        count[num] = 1 + count.get(num, 0)

    arr = []
    for num, cnt in count.items():
        arr.append([cnt, num])
    arr.sort()

    res = []
    while len(res) < k:
        res.append(arr.pop()[1])
    return res

```
### Time & Space Complexity
- Time complexity: O(nlogn)
- Space complexity: O(n)
---

## 3. Bucket Sort

```python

def topKFrequent(nums, k):
    count = {}
    for n in nums:
        count[n] = 1 + count.get(n, 0)
    
    # Bucket List
    freq = [[] for i in range(len(nums) + 1)]
    # ekhane 1 add kora hocce karon 0 position e kono data kokono takbena. karon je kono number at least 1 ta takbei. tai index 0 bad dia extra 1 ta index last e add kora hocce

    for n, c for count.items():
        freq[c].append(n)

    res = []

    for i in range(len(freq) - 1, 0, -1):
        # ekhane -1 kora hocce karon 0 index ta bad dia len(nums) er soman kora hocce. echarao 0 index escip kora hocce. r -1 bolte 1 porjonto jabe. er pore jabena.
        for n in freq[i]:
            res.append(n)
            if len(res) == k:
                return res

```

---
### Time & Space Complexity
- Time complexity: O(n)
- Space complexity: O(n)
---