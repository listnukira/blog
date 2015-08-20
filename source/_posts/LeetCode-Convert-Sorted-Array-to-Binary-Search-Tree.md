title: "[LeetCode] Convert Sorted Array to Binary Search Tree"
date: 2014-12-29 23:42:01
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Depth-first Search
---
把排序過的陣列轉成平衡的二元搜尋樹

<!-- more -->

### Solution

從陣列的中間開始新增節點，接著遞迴建立左子樹和右子樹，因為每次都是從中間新增節點，所以最後建立出來的二元樹高度會是平衡的

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
    TreeNode *sortedArrayToBST(vector<int> &num) {
        return sortedArrayToBST(num, 0, num.size() - 1);
    }

    TreeNode *sortedArrayToBST(vector<int> &num, int left, int right) {
        if (left > right)
            return NULL;

        int mid = (left + right) / 2;
        TreeNode *node = new TreeNode(num[mid]);

        node->left = sortedArrayToBST(num, left, mid - 1);
        node->right = sortedArrayToBST(num, mid + 1, right);

        return node;
    }
};
```
