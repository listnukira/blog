title: "[LeetCode] Binary Tree Level Order Traversal II"
date: 2014-12-04 14:44:05
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Breadth-first Search
---
延續 [Binary Tree Level Order Traversal](/-LeetCode-Binary-Tree-Level-Order-Traversal/)，這次要將結果反著放，所以 root 的值會在最後一個元素

<!-- more -->

###Solution 1

因為要把結果反著放，所以可以把 [Binary Tree Level Order Traversal](/-LeetCode-Binary-Tree-Level-Order-Traversal/) 得到的陣列反轉就是答案了，也就是將 `return ret;` 改成 `return vector<vector<int> >(ret.rbegin(), ret.rend());`

###Solution 2

因為第一個方法太取巧了，所以第二個方法稍微修改遞迴的程式碼，將原本從陣列最後面新增的 `vector<int>` 改成從陣列的開頭插入，將值放入陣列會根據 ret.size 和 level 來決定， level 大的會放在靠近陣列開頭的位置

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
    vector<vector<int> > levelOrderBottom(TreeNode *root) {
        ret.clear();
        levelOrderBottom(root, 0);
        return ret;
    }

    void levelOrderBottom(TreeNode *root, int level) {
        if (root == NULL)
            return;

        if (ret.size() == level)
            ret.insert(ret.begin(), vector<int>());

        levelOrderBottom(root->left, level + 1);
        levelOrderBottom(root->right, level + 1);

        ret[ret.size() - level - 1].push_back(root->val);
    }

private:
    vector<vector<int> > ret;
};
```
