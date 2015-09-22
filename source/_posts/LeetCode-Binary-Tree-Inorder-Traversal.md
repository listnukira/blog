title: '[LeetCode] Binary Tree Inorder Traversal'
date: 2015-09-21 11:30:05
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Stack
- Hash Table
---
傳回二元樹的中序排列

<!-- more -->

類似的題目: [Binary Tree Preorder Traversal](/LeetCode-Binary-Tree-Preorder-Traversal)

分別用遞迴，堆疊，Morris Traversal 三種方式實作

### Solution 1

第一個方法用遞迴

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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ret;

        inorderTraversal(root, ret);

        return ret;
    }

    void inorderTraversal(TreeNode* root, vector<int> &ret) {
        if (root == NULL)
            return;

        inorderTraversal(root->left, ret);
        ret.push_back(root->val);
        inorderTraversal(root->right, ret);
    }
};
```

### Solution 2

第二個方法用堆疊

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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ret;
        stack<TreeNode *> stacks;
        TreeNode *cur = root;

        while (cur || !stacks.empty()) {
            while (cur != NULL) {
                stacks.push(cur);
                cur = cur->left;
            }

            cur = stacks.top();
            stacks.pop();

            ret.push_back(cur->val);

            cur = cur->right;
        }

        return ret;
    }
};
```

### Solution 3

第三個方法用 Morris Traversal 方法，將目前左子樹最右邊的葉節點的 `right` 指標指向目前的節點，當左子樹都處理完之後，再改回 `NULL`，詳細說明可以參考這篇 [Morris Traversal](http://www.cnblogs.com/AnnieKim/archive/2013/06/15/MorrisTraversal.html)

這個方法只需要 O(1) 的空間，但同樣也能在 O(N) 的時間內完成

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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ret;
        TreeNode *cur = root, *prev = NULL;

        while (cur != NULL) {
            if (cur->left == NULL) {
                ret.push_back(cur->val);
                cur = cur->right;
            } else {
                prev = cur->left;

                while (prev->right != NULL && prev->right != cur)
                    prev = prev->right;

                if (prev->right == NULL) {
                    prev->right = cur;
                    cur = cur->left;
                } else {
                    prev->right = NULL;
                    ret.push_back(cur->val);
                    cur = cur->right;
                }
            }
        }

        return ret;
    }
};
```
