title: "[LeetCode] Binary Tree Preorder Traversal"
date: 2014-12-26 00:05:37
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Stack
---
給一個二元樹，傳回由前置式所表示的陣列

<!-- more -->

### Solution 1

第一個方法用遞迴

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
    vector<int> preorderTraversal(TreeNode *root) {
        vector<int> ret;
        preorderTraversal(ret, root);
        return ret;
    }

    void preorderTraversal(vector<int> &ret, TreeNode *root) {
        if (root == NULL)
            return;

        ret.push_back(root->val);
        preorderTraversal(ret, root->left);
        preorderTraversal(ret, root->right);
    }
};
```

### Solution 2

第二個方法用迭代，用到一個堆疊暫存

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
    vector<int> preorderTraversal(TreeNode *root) {
        vector<int> ret;
        stack<TreeNode *> s;

        if (root == NULL)
            return ret;

        s.push(root);
        while (!s.empty()) {
            TreeNode *top = s.top();
            s.pop();

            ret.push_back(top->val);
            if (top->right)
                s.push(top->right);
            if (top->left)
                s.push(top->left);
        }

        return ret;
    }
};
```
