title: "[LeetCode] Path Sum II"
date: 2014-10-03 22:58:44
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Depth-first Search
---
給一個二元樹 binary tree 還有一個總合 sum，找出所有從 root 到 leaf 的數字加總等於 sum 的路徑

<!-- more -->

###Solution

利用遞迴，大致流程如下

1. 把值放進 path 陣列的最後面
2. 如果是 leaf 而且加總等於 sum，這時 path 陣列的值就代表一組可能的路徑，把 path 放到 allPath 裡
3. 不是 leaf 就繼續往下遞迴，先往左邊再往右邊，遞迴得到的結果放到 allPath 裡
4. 把剛剛放在 path 陣列的值刪掉，回傳 allPath

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
    vector<vector<int> > pathSum(TreeNode *root, int sum) {
        vector< vector<int> > allPath, leftPath, rightPath;

        if (root == NULL)
            return allPath;

        path.push_back(root->val);

        if ((sum - root->val) == 0 && root->left == NULL && root->right == NULL) {
            allPath.push_back(path);
        } else {
            leftPath = pathSum(root->left, sum - root->val);
            rightPath = pathSum(root->right, sum - root->val);
            
            for (auto&& v : leftPath)
                allPath.push_back(v);
            for (auto&& v : rightPath)
                allPath.push_back(v);
        }

        path.pop_back();

        return allPath;
    }
private:
    vector<int> path;
};
```
