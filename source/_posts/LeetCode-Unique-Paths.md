title: "[LeetCode] Unique Paths"
date: 2015-05-02 17:17:07
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Dynamic Programming
---

給一個 m x n 的迷宮，算出從左上到右下總共有幾種走法

<!-- more -->

### Solution 1

第一個方法用組合數來算，總共會往下走 `m - 1` 步，往右走 `n - 1` 步，加起來 `m + n - 2` 步，所以最後要算的答案就是 `C(m + n - 2, m - 1) or C(m + n - 2, n - 1)`

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        long long int value = 1;

        if (m == 0 || n == 0)
            return 0;

        int A = m + n - 2;
        int B = min(m - 1, n - 1);
        for (int i = 1; i <= B; i++)
            value = value * A-- / i;

        return static_cast<int>(value);
    }
};
```

### Solution 2

第二個方法用 DP 遞迴的方式來做，座標 `(m, n)` 可以到達的方式可以由上面和左邊的數字加起來

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector< vector<int> > table(m, vector<int>(n, 0));

        return compute(table, m - 1, n - 1);
    }

    int compute(vector< vector<int> > &table, int m, int n) {
        if (m == 0 || n == 0)
            return 1;

        if (table[m][n] == 0)
            table[m][n] = compute(table, m - 1, n) + compute(table, m, n - 1);

        return table[m][n];
    }
};
```
