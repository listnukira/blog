title: "[LeetCode] Minimum Depth of Binary Tree"
date: 2014-12-05 00:22:36
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Depth-first Search
---
找出二元樹的最小深度，最小深度的意思是從根節點到最接近的葉節點長度

<!-- more -->

### Solution

因為要判斷最小根節點到最接近的葉節點長度，所以在遞迴的過程中，要分別判斷左右子樹是否為 NULL，NULL 則跳過

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
    int minDepth(TreeNode *root) {
        if (root == NULL)
            return 0;

        if (root->left == NULL)
            return minDepth(root->right) + 1;
        else if (root->right == NULL)
            return minDepth(root->left) + 1;
        else
            return min(minDepth(root->left), minDepth(root->right)) + 1;
    }
};
```
