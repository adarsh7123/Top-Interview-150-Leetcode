
---

# Valid Sudoku

## Problem Description

Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:
- Each row must contain the digits 1-9 without repetition.
- Each column must contain the digits 1-9 without repetition.
- Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.

## Examples

**Example 1:**

Input:
```
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
```

Output:
```
true
```

**Example 2:**

Input:
```
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
```

Output:
```
false
```

Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.

## Constraints

- `board.length == 9`
- `board[i].length == 9`
- `board[i][j] is a digit 1-9 or '.'`.

## Algorithm

The solution checks each row, column, and sub-box of the Sudoku board separately. For each row and column, it uses an unordered set to keep track of the digits encountered. For each sub-box, it uses a vector of unordered sets to keep track of the digits. If any digit is repeated in a row, column, or sub-box, the board is considered invalid.

## Code Implementation

```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        // Check each row
        for (int i = 0; i < 9; i++) {
            unordered_set<char> check;
            for (int j = 0; j < 9; j++) {
                if (board[i][j] != '.' && check.find(board[i][j]) != check.end()) {
                    return false;
                }
                check.insert(board[i][j]);
            }
        }

        // Check each column
        for (int j = 0; j < 9; j++) {
            unordered_set<char> check1;
            for (int i = 0; i < 9; i++) {
                if (board[i][j] != '.' && check1.find(board[i][j]) != check1.end()) {
                    return false;
                }
                check1.insert(board[i][j]);
            }
        }

        // Check each sub-box
        vector<unordered_set<char>> check_subbox(9); // 9 unordered sets
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                int loc = (i / 3) * 3 + j / 3; // Determine the sub-box grid
                if (board[i][j] != '.' && check_subbox[loc].find(board[i][j]) != check_subbox[loc].end()) {
                    return false;
                }
                check_subbox[loc].insert(board[i][j]);
            }
        }

        return true;
    }
};
```

---
