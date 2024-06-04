# Same Tree

## Problem Statement

Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

### Example 1:

```
Input: p = [1,2,3], q = [1,2,3]
Output: true
```

### Example 2:

```
Input: p = [1,2], q = [1,null,2]
Output: false
```

### Example 3:

```
Input: p = [1,2,1], q = [1,1,2]
Output: false
```

### Constraints:

- The number of nodes in both trees is in the range [0, 100].
- -10^4 <= Node.val <= 10^4

## Solution

To determine if two binary trees are the same, we need to check the following:

1. Both nodes are `NULL`, in which case they are the same.
2. One node is `NULL` and the other is not, in which case they are not the same.
3. Both nodes are not `NULL`, and their values are equal. Additionally, their left and right subtrees must also be the same.

Here's the C++ implementation of the solution:

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
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (!p && !q)
            return true;
        if ((p && !q) || (!p && q))
            return false;
        if (p->val != q->val)
            return false;
        return (isSameTree(p->left, q->left) && isSameTree(p->right, q->right));
    }
};
```

### Explanation:

1. **Base Case**:
   - If both nodes `p` and `q` are `NULL`, then the trees are the same (return `true`).
   - If one node is `NULL` and the other is not, then the trees are not the same (return `false`).

2. **Recursive Case**:
   - Check if the values of nodes `p` and `q` are equal. If not, return `false`.
   - Recursively check the left subtrees (`p->left` and `q->left`).
   - Recursively check the right subtrees (`p->right` and `q->right`).
   - Both the left and right subtrees must be the same for the trees to be considered the same.

### Complexity Analysis:

- **Time Complexity**: O(N), where N is the number of nodes in the trees. Each node is visited once.
- **Space Complexity**: O(H), where H is the height of the trees. This is due to the recursion stack, which will have at most H function calls at a time.

This approach ensures that we efficiently and correctly determine if two binary trees are structurally identical and have the same node values.