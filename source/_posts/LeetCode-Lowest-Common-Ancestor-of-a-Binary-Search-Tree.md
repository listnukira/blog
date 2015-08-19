title: '[LeetCode] Lowest Common Ancestor of a Binary Search Tree'
date: 2015-08-15 10:46:14
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
toc: false
---
找出樹的兩個節點間的共同祖先

<!-- more -->

從根節點開始，如果 `p`，`q` 都在同一邊，這個節點就一定不是共同祖先，就往下一個節點找，因為是二元搜尋樹，所以判斷是不是同一邊只要簡單的比較大小

###Solution

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root->val > p->val && root->val > q->val)
            return lowestCommonAncestor(root->left, p, q);
        else if (root->val < p->val && root->val < q->val)
            return lowestCommonAncestor(root->right, p, q);

        return root;
    }
};
```
