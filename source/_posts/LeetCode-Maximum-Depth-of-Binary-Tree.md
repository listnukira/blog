title: "[LeetCode] Maximum Depth of Binary Tree"
date: 2014-09-21 15:22:41
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Depth-first Search
---
給一個 binary tree，找出 maximum depth

<!-- more -->

### Solution

練習 DFS 的簡單題目

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
    int maxDepth(TreeNode *root) {
        if (root == NULL)
            return 0;

        return 1 + max(maxDepth(root->left), maxDepth(root->right));
    }
};
```
