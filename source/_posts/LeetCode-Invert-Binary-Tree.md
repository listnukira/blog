title: '[LeetCode] Invert Binary Tree'
date: 2015-07-07 10:50:58
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
---
將二元樹反轉，所有節點左右交換

<!-- more -->

分別用遞迴和迭代來實作

###Solution 1

第一個方法用遞迴

``` c++
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
    TreeNode* invertTree(TreeNode* root) {
        TreeNode *tmpNode;

        if (root) {
          tmpNode = root->left;
          root->left = invertTree(root->right);
          root->right = invertTree(tmpNode);
        }

        return root;
    }
};
```

###Solution 2

第二個方法用 queue 來存要處理的節點，將左右節點交換後就從 queue 中刪除

``` c++
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
    TreeNode* invertTree(TreeNode* root) {
        queue<TreeNode *> s;
        TreeNode *tmpNode;

        s.push(root);
        while(!s.empty()) {
            if (s.front() == NULL) {
                s.pop();
                continue;
            }

            s.push(s.front()->left);
            s.push(s.front()->right);

            tmpNode = s.front()->left;
            s.front()->left = s.front()->right;
            s.front()->right = tmpNode;

            s.pop();
        }

        return root;
    }
};
```
