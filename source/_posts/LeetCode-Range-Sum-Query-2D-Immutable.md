title: '[LeetCode] Range Sum Query 2D - Immutable'
date: 2015-12-28 23:57:25
categories: LeetCode
tags:
- LeetCode
- C/C++
- Dynamic Programming
toc: false
---
給一個整數二維陣列，算出由任意兩點組成矩陣的和

<!-- more -->

[Range Sum Query - Immutable](/LeetCode-Range-Sum-Query-Immutable) 的二維版本

另外用一個二維陣列 sums 存矩陣的和，`sums[i][j]` 代表從 (0, 0) 到 (i, j) 的總和，`sums[i][j]` 的算法跟算聯集的計算方法差不多，[Discuss](https://leetcode.com/discuss/69424/clean-c-solution-and-explaination-o-mn-space-with-o-1-time) 裡有詳細的說明，要算任意兩點組成矩陣的和時也是同樣的想法

### Solution

```c++
class NumMatrix {
public:
    NumMatrix(vector<vector<int>> &matrix) {
        int row = matrix.size();
        int col = (row != 0) ? matrix[0].size() : 0;

        sums = vector<vector<int>>(row + 1, vector<int>(col + 1, 0));

        for (int i = 1; i <= row; i++) {
            for (int j = 1; j <= col; j++) {
                sums[i][j] = matrix[i - 1][j - 1] + sums[i - 1][j] + sums[i][j - 1] - sums[i - 1][j - 1];
            }
        }
    }

    int sumRegion(int row1, int col1, int row2, int col2) {
        return sums[row2 + 1][col2 + 1] - sums[row2 + 1][col1] - sums[row1][col2 + 1] + sums[row1][col1];
    }
private:
    vector<vector<int>> sums;
};
```
