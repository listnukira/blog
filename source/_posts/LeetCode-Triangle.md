title: "[LeetCode] Triangle"
date: 2014-12-22 22:34:59
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Dynamic Programming
---
給一個三角型陣列，算出由上到下的路徑中，加總最小的一條

<!-- more -->

### Solution 1

第一個方法在原本的資料上做計算，不會用到額外的空間

``` c++
class Solution {
public:
    int minimumTotal(vector<vector<int> > &triangle) {
        for (int i = triangle.size() - 2; i >= 0; --i) {
            for (int j = 0; j <= i; ++j) {
                triangle[i][j] = min(triangle[i + 1][j], triangle[i + 1][j + 1]) + triangle[i][j];
            }
        }

        return triangle[0][0];
    }
};
```

### Solution 2

第二個方法不會修改到原本的資料，改用一個一維的陣列 DP，初始設定成三角形最底層那一列，接著從倒數第二層開始更新 DP，最後 DP[0] 即是最小的總合

``` c++
ass Solution {
public:
    int minimumTotal(vector<vector<int> > &triangle) {
        vector<int> DP(triangle.back());

        for (int i = triangle.size() - 2; i >= 0; --i) {
            for (int j = 0; j <= i; ++j) {
                DP[j] = min(DP[j], DP[j + 1]) + triangle[i][j];
            }
        }

        return DP[0];
    }
};
```
