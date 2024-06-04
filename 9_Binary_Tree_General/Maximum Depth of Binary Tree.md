# Maximum Depth of Binary Tree

## Problem Statement

Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

### Example 1:

```
Input: root = [3,9,20,null,null,15,7]
Output: 3
```

### Example 2:

```
Input: root = [1,null,2]
Output: 2
```

### Constraints:

- The number of nodes in the tree is in the range [0, 10^4].
- -100 <= Node.val <= 100

## Solution

The solution to find the maximum depth of a binary tree involves using a recursive approach. We can define the depth of a node as 1 plus the maximum depth of its left and right subtrees. If the node is `NULL`, its depth is 0.

Here is the C++ implementation:

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
    int maxDepth(TreeNode* root) {
        if (root == NULL) return 0;
        
        int left = maxDepth(root->left);
        int right = maxDepth(root->right);
        
        int ans = max(left, right) + 1;
        return ans;
    }
};
```

### Explanation:

1. **Base Case**: If the root is `NULL`, the depth is 0.
2. **Recursive Case**:
   - Compute the maximum depth of the left subtree.
   - Compute the maximum depth of the right subtree.
   - The depth of the current node is 1 plus the maximum of the depths of the left and right subtrees.

### Complexity Analysis:

- **Time Complexity**: O(N), where N is the number of nodes in the binary tree. Each node is visited once.
- **Space Complexity**: O(H), where H is the height of the binary tree. This is due to the recursion stack, which will have at most H function calls at a time.

This solution ensures that we efficiently calculate the maximum depth of the binary tree by leveraging the properties of recursion and the definition of tree depth.