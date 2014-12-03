title: "[LeetCode] Symmetric Tree"
date: 2014-12-03 15:06:05
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Depth-first Search
---
判斷兩個樹是否對稱

<!-- more -->

###Solution

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
    bool isSymmetric(TreeNode *root) {
        return (root) ? isSymmetric(root->left, root->right) : true;
    }
    
    bool isSymmetric(TreeNode *l, TreeNode *r) {
        if (l == NULL || r == NULL)
            return (l == r);

        return (l->val == r->val) &&
            isSymmetric(l->left, r->right) &&
            isSymmetric(l->right, r->left);
    }
};
```
