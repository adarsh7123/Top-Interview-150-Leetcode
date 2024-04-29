

---

# Spiral Matrix

## Problem Description

Given an `m x n` matrix, return all elements of the matrix in spiral order.

## Examples

**Example 1:**

Input:
```
[[1,2,3],
 [4,5,6],
 [7,8,9]]
```

Output:
```
[1,2,3,6,9,8,7,4,5]
```

**Example 2:**

Input:
```
[[1,2,3,4],
 [5,6,7,8],
 [9,10,11,12]]
```

Output:
```
[1,2,3,4,8,12,11,10,9,5,6,7]
```

## Constraints

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 10`
- `-100 <= matrix[i][j] <= 100`

## Algorithm

The solution traverses the matrix in a spiral order, starting from the top-left corner and moving clockwise until all elements are visited. It maintains four pointers representing the boundaries of the current spiral layer: `startingrow`, `startingcol`, `endingrow`, and `endingcol`. It iterates through each layer, adding elements to the result vector `ans` in the specified order. The process continues until all elements are added to `ans`.

## Code Implementation

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> ans; 
        int row = matrix.size();
        int col = matrix[0].size();
        int count = 0;
        int total = row * col;        

        int startingrow = 0;
        int startingcol = 0;
        int endingrow = row - 1;
        int endingcol = col - 1;

        while (count < total) {
            for (int i = startingcol; count < total && i <= endingcol; i++) {
                ans.push_back(matrix[startingrow][i]);
                count++;
            }
            startingrow++;

            for (int i = startingrow; count < total && i <= endingrow; i++) {
                ans.push_back(matrix[i][endingcol]);
                count++;
            }
            endingcol--;

            for (int i = endingcol; count < total && i >= startingcol; i--) {
                ans.push_back(matrix[endingrow][i]);
                count++;
            }
            endingrow--;

            for (int i = endingrow; count < total && i >= startingrow; i--) {
                ans.push_back(matrix[i][startingcol]);
                count++;
            }
            startingcol++;
        }

        return ans;
    }
};
```

---
