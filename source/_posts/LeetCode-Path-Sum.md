title: "[LeetCode] Path Sum"
date: 2014-10-02 22:52:44
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Depth-first Search
---
給一個二元樹 binary tree 還有一個總合 sum，判斷是否有一條從 root 到 leaf 的路徑，數字加總等於 sum

<!-- more -->

### Solution

``` c++
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool hasPathSum(TreeNode *root, int sum) {
        if (root == NULL)
            return false;

        if (root->left == NULL && root->right == NULL)
            return (sum - root->val == 0);

        return hasPathSum(root->left, sum - root->val) || hasPathSum(root->right, sum - root->val);
    }
};
```
