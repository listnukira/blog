title: "[LeetCode] Binary Tree Level Order Traversal"
date: 2014-12-04 13:44:35
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Breadth-first Search
---
將一顆樹以 level order 的順序放入一個二維陣列，root 會是陣列的第一個元素

<!-- more -->

###Solution

二維陣列 ret 代表最後要回傳的陣列，當 ret.size 等於 level 時，代表目前所在的 level 之前並沒有到過，所以新增一個一維陣列進 ret，接著根據 level 將值放到不同的陣列，最後 ret 便會根據 level order 的順序擺放

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
    vector<vector<int> > levelOrder(TreeNode *root) {
        ret.clear();
        levelOrder(root, 0);
        return ret;
    }

    void levelOrder(TreeNode *root, int level) {
        if (root == NULL)
            return;

        if (ret.size() == level)
            ret.push_back(vector<int>());

        ret[level].push_back(root->val);

        levelOrder(root->left, level + 1);
        levelOrder(root->right, level + 1);
    }

private:
    vector<vector<int> > ret;
};
```
