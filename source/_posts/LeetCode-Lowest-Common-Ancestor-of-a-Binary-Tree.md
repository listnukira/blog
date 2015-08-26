title: '[LeetCode] Lowest Common Ancestor of a Binary Tree'
date: 2015-08-23 22:33:31
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
toc: false
---
找出二元樹兩個節點間的共同祖先

<!-- more -->

從根節點開始，遞迴的找出 `p`，`q` 是在左子樹還是右子樹，這時只會有兩種狀況

1. `p`，`q` 在不同邊，`leftParent` 跟 `rightParent` 都會有值，代表這個點就是共同祖先
2. `p`，`q` 在同一邊，`leftParent` 跟 `rightParent` 只會有一個有值，回傳有值的那個

### Solution

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
        if (root == NULL || root == p || root == q)
            return root;

        TreeNode *leftParent = lowestCommonAncestor(root->left, p, q);
        TreeNode *rightParent = lowestCommonAncestor(root->right, p, q);
        if (leftParent && rightParent)
            return root;
        else
            return leftParent ? leftParent : rightParent;
    }
};
```
