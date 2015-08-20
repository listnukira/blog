title: "[LeetCode] Balanced Binary Tree"
date: 2014-12-05 13:58:28
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Depth-first Search
---
判斷一個二元樹是不是平衡的

<!-- more -->

### Solution 1

要判斷二元樹是不是平衡的，有兩個條件

1. 左右子樹的高度差小於等於 1
2. 左右子樹都是平衡的

根據這兩個條件可以寫出以下的程式碼，height 函式計算高度，isBalanced 函式判斷是不是平衡樹

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
    bool isBalanced(TreeNode *root) {
        if (root == NULL)
            return true;

        return (abs(height(root->left) - height(root->right)) < 2 ) &&
            isBalanced(root->left) &&
            isBalanced(root->right);
    }

    int height(TreeNode *root) {
        if (root == NULL)
            return 0;

        return max(height(root->left), height(root->right)) + 1;
    }
};
```

### Solution 2

第一個方法 height 和 isBalanced 函式都會跑遞迴，所以第二個方法把判斷是不是平衡樹當成一個變數，將兩個遞迴函式變成一個，isBalancedDFS 會回傳高度，參數 isBalance 用來判斷是不是平衡樹

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
    bool isBalanced(TreeNode *root) {
        bool isBalance = true;
        isBalancedDFS(root, isBalance);
        return isBalance;
    }

    int isBalancedDFS(TreeNode *root, bool &isBalance) {
        if (root == NULL)
            return 0;

        int heightL = isBalancedDFS(root->left, isBalance);
        int heightR = isBalancedDFS(root->right, isBalance);
        
        if (abs(heightL - heightR) > 1)
            isBalance = false;

        return max(heightL, heightR) + 1;
    }
};
```
