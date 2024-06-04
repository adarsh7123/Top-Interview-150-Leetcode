# Surrounded Regions

## Problem Statement

Given an m x n matrix `board` containing 'X' and 'O', capture all regions that are 4-directionally surrounded by 'X'. A region is captured by flipping all 'O's into 'X's in that surrounded region.

### Example 1:

```
Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
Explanation: 
Notice that an 'O' should not be flipped if:
- It is on the border, or
- It is adjacent to an 'O' that should not be flipped.
The bottom 'O' is on the border, so it is not flipped.
The other three 'O' form a surrounded region, so they are flipped.
```

### Example 2:

```
Input: board = [["X"]]
Output: [["X"]]
```

### Constraints:

- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 200`
- `board[i][j]` is 'X' or 'O'.

## Solution

To solve the problem, we can use a Depth-First Search (DFS) approach to mark all 'O's that are not surrounded by 'X's because they are connected to the boundary. We will convert these 'O's to a temporary character (e.g., '#'). After marking, we can flip all the remaining 'O's to 'X's and revert the temporary characters back to 'O's.

### Implementation

Here's the C++ implementation of the solution:

```cpp
class Solution {
public:
    void DFS(vector<vector<char>>& board, int i, int j, int m, int n) {
        if (i < 0 || j < 0 || i >= m || j >= n || board[i][j] != 'O') return;
        board[i][j] = '#';
        DFS(board, i - 1, j, m, n);
        DFS(board, i + 1, j, m, n);
        DFS(board, i, j - 1, m, n);
        DFS(board, i, j + 1, m, n);
    }

    void solve(vector<vector<char>>& board) {
        int row = board.size();
        if (row == 0) return;

        int col = board[0].size();

        // Moving in boundary columns
        for (int i = 0; i < row; i++) {
            if (board[i][0] == 'O') {
                DFS(board, i, 0, row, col);
            }
            if (board[i][col - 1] == 'O') {
                DFS(board, i, col - 1, row, col);
            }
        }

        // Moving in boundary rows
        for (int i = 0; i < col; i++) {
            if (board[0][i] == 'O') {
                DFS(board, 0, i, row, col);
            }
            if (board[row - 1][i] == 'O') {
                DFS(board, row - 1, i, row, col);
            }
        }

        // Flipping 'O' to 'X' and '#' back to 'O'
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (board[i][j] == 'O') {
                    board[i][j] = 'X';
                }
                if (board[i][j] == '#') {
                    board[i][j] = 'O';
                }
            }
        }
    }
};
```

### Explanation:

1. **Helper Function `DFS`**:
   - **Parameters**:
     - `vector<vector<char>>& board`: the game board.
     - `int i`: current row index.
     - `int j`: current column index.
     - `int m`: total number of rows.
     - `int n`: total number of columns.
   - **Base Case**: If the current cell is out of bounds or not an 'O', return.
   - **Mark the current cell**: Change 'O' to '#'.
   - **Recursively apply DFS**: Check all four directions (up, down, left, right).

2. **Main Function `solve`**:
   - Initialize the number of rows (`row`) and columns (`col`).
   - Perform DFS for all boundary 'O's:
     - Iterate through the first and last column for each row.
     - Iterate through the first and last row for each column.
   - After marking the boundary-connected 'O's, iterate through the board:
     - Change remaining 'O's to 'X'.
     - Change '#' back to 'O'.

### Complexity Analysis:

- **Time Complexity**: O(m * n), where m is the number of rows and n is the number of columns in the board. We potentially visit each cell once.
- **Space Complexity**: O(m * n) in the worst case due to the recursion stack during the DFS calls.

This approach efficiently marks and flips the regions, ensuring that the surrounded regions are correctly captured.