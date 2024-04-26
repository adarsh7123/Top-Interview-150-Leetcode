
---

## 931. Minimum Falling Path Sum

Given an n x n array of integers `matrix`, return the minimum sum of any falling path through the matrix.

A falling path starts at any element in the first row and chooses the element in the next row that is either directly below or diagonally left/right. Specifically, the next element from position `(row, col)` will be `(row + 1, col - 1)`, `(row + 1, col)`, or `(row + 1, col + 1)`.

### Example 1:

**Input:**
```
matrix = [[2,1,3],[6,5,4],[7,8,9]]
```

**Output:**
```
13
```

**Explanation:**
There are two falling paths with a minimum sum as shown.

### Example 2:

**Input:**
```
matrix = [[-19,57],[-40,-5]]
```

**Output:**
```
-59
```

**Explanation:**
The falling path with a minimum sum is shown.

### Constraints:

- `n == matrix.length == matrix[i].length`
- `1 <= n <= 100`
- `-100 <= matrix[i][j] <= 100`

### Solution:

```cpp
class Solution {
public:
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int n = matrix.size();    // Number of rows in the matrix
        int m = matrix[0].size(); // Number of columns in the matrix

        vector<int> prev(m, 0); // Represents the previous row's maximum path sums
        vector<int> cur(m, 0); // Represents the current row's maximum path sums

        // Initialize the first row (base condition)
        for (int j = 0; j < m; j++) {
            prev[j] = matrix[0][j];
        }

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < m; j++) {
                // Calculate the maximum path sum for the current cell
                // considering three possible directions: up, left diagonal, and
                // right diagonal

                // Up direction
                int up = matrix[i][j] + prev[j];

                // Left diagonal direction (if it's a valid move)
                int leftDiagonal = matrix[i][j];
                if (j - 1 >= 0) {
                    leftDiagonal += prev[j - 1];
                } else {
                    leftDiagonal += 1e9; // A very large negative value to
                                          // represent an invalid path
                }

                // Right diagonal direction (if it's a valid move)
                int rightDiagonal = matrix[i][j];
                if (j + 1 < m) {
                    rightDiagonal += prev[j + 1];
                } else {
                    rightDiagonal += 1e9; // A very large negative value to
                                           // represent an invalid path
                }

                // Store the maximum of the three paths in the current row
                cur[j] = min(up, min(leftDiagonal, rightDiagonal));
            }

            // Update the 'prev' array with the values from the 'cur' array for
            // the next iteration
            prev = cur;
        }

        // Find the maximum value in the last row of 'prev', which represents
        // the maximum path sums ending at each cell
        int mini = INT_MAX;
        for (int j = 0; j < m; j++) {
            mini = min(mini, prev[j]);
        }

        // The maximum path sum is the maximum value in the last row of 'prev'
        return mini;
    }
};
```

---
