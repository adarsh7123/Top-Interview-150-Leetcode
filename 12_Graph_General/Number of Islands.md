# Number of Islands

## Problem Statement

Given an m x n 2D binary grid `grid` which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

### Example 1:

```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

### Example 2:

```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

### Constraints:

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j]` is '0' or '1'.

## Solution

To determine the number of islands, we can use Depth-First Search (DFS). We'll traverse the grid, and each time we find a '1', we'll start a DFS to mark all connected '1's as visited by changing them to '0'. Each DFS corresponds to one island.

### Implementation

Here is the C++ implementation:

```cpp
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        if (grid.empty() || grid[0].empty()) {
            return 0;
        }

        int islands = 0;
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid[0].size(); j++) {
                if (grid[i][j] == '1') {
                    islands++;
                    dfs(grid, i, j);
                }
            }
        }
        return islands;
    }

private:
    void dfs(vector<vector<char>>& grid, int i, int j) {
        if (i < 0 || i >= grid.size() || j < 0 || j >= grid[0].size() || grid[i][j] != '1') {
            return;
        }

        grid[i][j] = '0'; // mark as visited

        dfs(grid, i + 1, j);
        dfs(grid, i - 1, j);
        dfs(grid, i, j + 1);
        dfs(grid, i, j - 1);
    }
};
```

### Explanation

1. **Main Function `numIslands`**:
   - **Parameters**:
     - `vector<vector<char>>& grid`: The 2D grid representing the map.
   - **Logic**:
     - Initialize `islands` to count the number of islands.
     - Traverse each cell in the grid. If a cell contains '1', increment the island count and start a DFS from that cell to mark all connected '1's as visited.
     - Return the total number of islands.

2. **Helper Function `dfs`**:
   - **Parameters**:
     - `vector<vector<char>>& grid`: The 2D grid.
     - `int i`: Current row index.
     - `int j`: Current column index.
   - **Base Case**: If the current cell is out of bounds or not '1', return.
   - **Mark the current cell as visited**: Change '1' to '0'.
   - **Recursive Calls**: Move in all four directions (up, down, left, right) and perform DFS.

### Complexity Analysis

- **Time Complexity**: O(m * n), where m is the number of rows and n is the number of columns in the grid. We potentially visit each cell once.
- **Space Complexity**: O(m * n) in the worst case due to the recursion stack during the DFS calls.

This approach ensures that we efficiently count and mark islands, ensuring all connected '1's are properly identified and marked as visited.