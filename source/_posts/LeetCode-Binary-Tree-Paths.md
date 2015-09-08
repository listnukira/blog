title: '[LeetCode] Binary Tree Paths'
date: 2015-09-08 13:46:17
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Depth-first Search
---
印出每個從根節點到葉節點的路徑

<!-- more -->

分別用遞迴還有迭代來做

### Solution 1

第一個方法用遞迴，把存有目前路徑字串的陣列與目前路徑字串跟著遞迴傳遞

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
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> ret;

        if (root != NULL)
            binaryTreePaths(root, ret, to_string(root->val));

        return ret;
    }

    void binaryTreePaths(TreeNode* root, vector<string> &ret, string s) {
        if (root->left)
            binaryTreePaths(root->left, ret, s + "->" + to_string(root->left->val));

        if (root->right)
            binaryTreePaths(root->right, ret, s + "->" + to_string(root->right->val));

        if (root->left == NULL && root->right == NULL)
            ret.push_back(s);
    }
};
```

### Solution 2

第二個方法用結構把節點跟字串包起來存入堆疊

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

struct PathNode {
    TreeNode *node;
    string str;
};

class Solution {
public:
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> ret;
        stack<struct PathNode> nodes;

        if (root == NULL)
            return ret;

        nodes.push({root, to_string(root->val)});
        while (!nodes.empty()) {
            TreeNode *tmpNode = nodes.top().node;
            string s = nodes.top().str;
            nodes.pop();

            if (tmpNode->right)
                nodes.push({tmpNode->right, s + "->" + to_string(tmpNode->right->val)});
            if (tmpNode->left)
                nodes.push({tmpNode->left, s + "->" + to_string(tmpNode->left->val)});

            if (tmpNode->left == NULL && tmpNode->right == NULL)
                ret.push_back(s);
        }

        return ret;
    }
};
```
