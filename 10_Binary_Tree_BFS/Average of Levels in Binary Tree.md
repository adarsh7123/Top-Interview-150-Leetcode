# Average of Levels in Binary Tree

## Problem Statement

Given the root of a binary tree, return the average value of the nodes on each level in the form of an array. Answers within \(10^{-5}\) of the actual answer will be accepted.

### Example 1:

```
Input: root = [3,9,20,null,null,15,7]
Output: [3.00000,14.50000,11.00000]
Explanation: The average value of nodes on level 0 is 3, on level 1 is 14.5, and on level 2 is 11.
Hence return [3, 14.5, 11].
```

### Example 2:

```
Input: root = [3,9,20,15,7]
Output: [3.00000,14.50000,11.00000]
```

### Constraints:

- The number of nodes in the tree is in the range [1, 10^4].
- \(-2^{31} \leq \text{Node.val} \leq 2^{31} - 1\)

## Solution

To compute the average value of the nodes on each level of a binary tree, we can perform a level-order traversal (BFS). In each level, we calculate the sum of the node values and then divide by the number of nodes at that level to get the average.

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
 *     TreeNode(int x) : val(x), left(nullptr, right(nullptr)) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<double> averageOfLevels(TreeNode* root) {
        vector<double> ans;
        queue<TreeNode*> q;
        q.push(root);
        while (!q.empty()) {
            int sz = q.size();
            double sum = 0;
            for (int i = 0; i < sz; i++) {
                TreeNode* node = q.front();
                q.pop();
                sum += node->val;
                if (node->left != NULL) q.push(node->left);
                if (node->right != NULL) q.push(node->right);
            }
            ans.push_back(sum / sz);
        }
        return ans;
    }
};
```

### Explanation:

1. **Initialization**:
   - Create a vector `ans` to store the average values.
   - Use a queue `q` to facilitate level-order traversal and initialize it with the root node.

2. **Level-order Traversal**:
   - While the queue is not empty, process each level of the tree:
     - Determine the number of nodes at the current level (`sz`).
     - Initialize `sum` to 0 for accumulating the sum of node values at the current level.
     - For each node in the current level:
       - Dequeue the node.
       - Add its value to `sum`.
       - Enqueue its left and right children if they exist.
     - Compute the average for the current level by dividing `sum` by `sz` and add it to `ans`.

3. **Return the result**:
   - After processing all levels, return the `ans` vector containing the average values for each level.

### Complexity Analysis:

- **Time Complexity**: O(N), where N is the number of nodes in the tree. Each node is visited once.
- **Space Complexity**: O(M), where M is the maximum number of nodes at any level in the tree. This accounts for the space used by the queue during the level-order traversal.

This approach ensures that we efficiently calculate the average values of the nodes at each level by leveraging a BFS traversal.