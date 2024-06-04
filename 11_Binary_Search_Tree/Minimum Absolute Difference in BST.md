# Minimum Absolute Difference in BST

## Problem Statement

Given the root of a Binary Search Tree (BST), return the minimum absolute difference between the values of any two different nodes in the tree.

### Example 1:

```
Input: root = [4,2,6,1,3]
Output: 1
```

### Example 2:

```
Input: root = [1,0,48,null,null,12,49]
Output: 1
```

### Constraints:

- The number of nodes in the tree is in the range [2, 10^4].
- 0 <= Node.val <= 10^5

## Solution

To find the minimum absolute difference between the values of any two different nodes in a BST, we can leverage the properties of BSTs. Specifically, an in-order traversal of a BST yields a sorted list of node values. The minimum absolute difference will then be the smallest difference between consecutive values in this sorted list.

### Implementation

Here's the C++ implementation of the solution:

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    void solve(TreeNode* root, vector<int>& temp) {
        if (root == NULL)
            return;

        solve(root->left, temp);
        temp.push_back(root->val);
        solve(root->right, temp);
    }

    int getMinimumDifference(TreeNode* root) {
        vector<int> temp;
        solve(root, temp);
        int mini = INT_MAX;

        for (int i = 0; i < temp.size() - 1; i++) {
            int tempo = temp[i + 1] - temp[i];
            mini = min(mini, tempo);
        }
        return mini;
    }
};
```

### Explanation:

1. **Helper Function `solve`**:
   - **Parameters**:
     - `TreeNode* root`: current node.
     - `vector<int>& temp`: vector to store node values in in-order.
   - **In-order Traversal**:
     - If the current node is `NULL`, return.
     - Recursively traverse the left subtree.
     - Add the current node's value to `temp`.
     - Recursively traverse the right subtree.

2. **Main Function `getMinimumDifference`**:
   - Initialize an empty vector `temp` to store the node values.
   - Call the `solve` function to perform in-order traversal and fill `temp`.
   - Initialize `mini` to `INT_MAX` to keep track of the minimum difference.
   - Iterate through the `temp` vector and compute the difference between consecutive elements.
   - Update `mini` with the smallest difference found.
   - Return `mini`.

### Complexity Analysis:

- **Time Complexity**: O(N), where N is the number of nodes in the tree. Each node is visited once during the in-order traversal, and calculating the minimum difference also requires iterating through the list of node values.
- **Space Complexity**: O(N), where N is the number of nodes in the tree. This accounts for the space used by the vector `temp` to store the node values.

This approach ensures that we efficiently find the minimum absolute difference between the values of any two different nodes in the BST by leveraging the properties of in-order traversal and the sorted nature of the resulting node values.