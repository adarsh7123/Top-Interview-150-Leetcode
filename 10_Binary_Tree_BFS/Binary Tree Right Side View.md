# Binary Tree Right Side View

## Problem Statement

Given the root of a binary tree, imagine yourself standing on the right side of it. Return the values of the nodes you can see ordered from top to bottom.

### Example 1:

```
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]
```

### Example 2:

```
Input: root = [1,null,3]
Output: [1,3]
```

### Example 3:

```
Input: root = []
Output: []
```

### Constraints:

- The number of nodes in the tree is in the range [0, 100].
- -100 <= Node.val <= 100

## Solution

To get the right side view of the binary tree, we can use a depth-first search (DFS) approach. The idea is to traverse the tree level by level and prioritize the right subtree over the left subtree. At each level, we record the first node encountered, which will be the rightmost node for that level.

Here's the C++ implementation:

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr, right(nullptr)) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    void solve(TreeNode* root, int lvl, vector<int>& ans) {
        if (root == NULL) return;

        if (ans.size() == lvl) {
            ans.push_back(root->val);
        }

        solve(root->right, lvl + 1, ans);
        solve(root->left, lvl + 1, ans);
    }

    vector<int> rightSideView(TreeNode* root) {
        vector<int> ans;
        int lvl = 0;
        solve(root, lvl, ans);
        return ans;
    }
};
```

### Explanation:

1. **Helper Function `solve`**:
   - **Parameters**: 
     - `TreeNode* root`: current node.
     - `int lvl`: current level in the tree.
     - `vector<int>& ans`: list to store the rightmost node values.
   - **Base Case**: If the current node is `NULL`, return.
   - **Recording Rightmost Node**: If the size of `ans` is equal to the current level, it means we haven't recorded a node for this level yet, so we add the current node's value to `ans`.
   - **Recursion**: First recurse on the right subtree, then on the left subtree to ensure rightmost nodes are recorded first.

2. **Main Function `rightSideView`**:
   - Initialize an empty vector `ans` to store the right side view.
   - Call the helper function `solve` with the root node and level 0.
   - Return the `ans` vector.

### Complexity Analysis:

- **Time Complexity**: O(N), where N is the number of nodes in the binary tree. Each node is visited once.
- **Space Complexity**: O(H), where H is the height of the tree. This accounts for the recursion stack which will have at most H function calls at any point.

This approach ensures that we correctly capture the right side view of the binary tree by leveraging depth-first traversal and recording nodes at each level in the correct order.