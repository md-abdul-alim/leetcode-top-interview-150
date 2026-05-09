


```python
def isValidSudoku(self, board: List[List[str]]) -> bool:
    rows = [0] * 9
    cols = [0] * 9
    squares = [0] * 9

    for r in range(9):
        for c in range(9):
            if board[r][c] == ".":
                continue

            val = int(board[r][c]) - 1 
            '''
            # Sudoku numbers are 1 → 9. But bit positions start from 0.

            board[r][c] = "5"
            val = 5 - 1 = 4

            Now bit position 4 represents number 5.
            '''

            '''
            Understanding 1 << val. << means left shift. It moves binary 1 to the left.
            like: 
                -> 1 << 0 -> Binary: 000000001, Represents number 1.
                -> 1 << 4 -> Binary: 000010000, Represents number 5.
                -> 1 << 8 -> Binary: 100000000, Represents number 9.

            '''

            if (1 << val) & rows[r]:
                return False
            if (1 << val) & cols[c]:
                return False
            if (1 << val) & squares[(r // 3) * 3 + (c // 3)]:
                return False

            '''
                Understanding |=. 
                |= means: a |= b or a = a | b
                It turns ON bits.

                Example: Suppose row currently has: 000010000 (number 5 exists).

                Now add number 3.
                1 << 2 = 000000100

                OR operation:

                000010000
                |
                000000100
                -----------
                000010100

                Now row contains both:
                -> 5
                -> 3

                So this line:
                rows[r] |= (1 << val)

                means:
                "Mark this number as seen in this row."

                Same for columns and squares.
            '''
            rows[r] |= (1 << val)
            cols[c] |= (1 << val)
            squares[(r // 3) * 3 + (c // 3)] |= (1 << val)

    return True
```
---

### Time & Space Complexity
- Time complexity: O(n^2) # as there are two nested loop
- Space complexity: O(3n) -> O(n), O(1) # as there are 3 hash set rows, cols, squares
---


Why Bit Manipulation is Fast.
Checking duplicates becomes:
    - O(1)
    - Very little memory
    - Faster than sets