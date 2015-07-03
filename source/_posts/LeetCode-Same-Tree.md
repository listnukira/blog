title: "[LeetCode] Same Tree"
date: 2014-09-03 00:51:02
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Depth-first Search
---
判斷兩顆樹是否相等

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
    bool isSameTree(TreeNode *p, TreeNode *q) {
        if (p == NULL || q == NULL)
            return (p == q);
            
        return (p->val == q->val) && isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
};
```
