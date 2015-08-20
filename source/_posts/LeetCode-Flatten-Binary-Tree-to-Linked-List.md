title: "[LeetCode] Flatten Binary Tree to Linked List"
date: 2014-12-23 23:10:48
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Depth-first Search
---
將一個二元樹轉成串列

<!-- more -->

範例

<pre>

              1
               \
                2
    1            \
   / \            3
  2   5   ==>      \
 / \   \            4
3   4   6            \
                      5
                       \
                        6

</pre>

### Solution 1

第一個方法用遞迴來實作，在每一次的遞迴會得到兩個指標 leftTail 和 rightTail，分別代表左右子樹轉成串列後的最尾端，根據這兩個指標調整樹的長相，最後遞迴會傳回整個串列的最尾端，如果 rightTail 不等於 NULL，則 rightTail 就是最尾端

流程如下

<pre>

    1            1          1
   / \          / \          \
  2   5   ==>  2   5   ==>    2
 / \   \        \   \          \
3   4   6        3   6          3
                  \              \
                   4              4
                                   \
                                    5
                                     \
                                      6

</pre>

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
    void flatten(TreeNode *root) {
        flat(root);
    }
    
    TreeNode *flat(TreeNode *root) {
        if (!root || (root->left == NULL && root->right == NULL))
            return root;

        TreeNode *leftTail = root->left ? flat(root->left) : NULL;
        TreeNode *rightTail = root->right ? flat(root->right) : NULL;

        if (leftTail) {
            leftTail->right = root->right;
            root->right = root->left;
            root->left = NULL;
        }

        return (rightTail ? rightTail : leftTail);
    }
};
```

### Solution 2

第二個方法與第一個方法想法差不多，但是改用非遞迴的方式寫

流程如下

<pre>

    1            1          1            1          1
   / \          /            \            \          \
  2   5   ==>  2       ==>    2      ==>   2    ==>   2
 / \   \      / \            / \          /            \
3   4   6    3   4          3   4        3              3
                  \              \        \              \
                   5              5        4              4
                    \              \        \              \
                     6              6        5              5
                                              \              \
                                               6              6

</pre>


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
    void flatten(TreeNode *root) {
        TreeNode *cur = root;

        while (cur) {
            if (cur->left) {
                TreeNode *tail = cur->left;
                while (tail->right)
                    tail = tail->right;

                tail->right = cur->right;
                cur->right = cur->left;
                cur->left = NULL;
            }

            cur = cur->right;
        }
    }
};
```
