title: "[LeetCode] Climbing Stairs"
date: 2014-12-03 16:14:16
categories: LeetCode
tags:
- LeetCode
- C/C++
- Dynamic Programming
---
爬一個 n 階的樓梯，每次只能移動一步或兩步，算出爬到第 n 階有幾種方法

<!-- more -->

### Solution

第 n 階的方法可以由 n - 1 階的方法數加上 n - 2 階的方法數所得到，所以本質上就是要計算 Fibonacci 數

``` c++
class Solution {
public:
    int climbStairs(int n) {
        int prev = 1, ans = 0;

        for (int i = 0; i <= n; i++) {
            int tmp = ans + prev;
            prev = ans;
            ans = tmp;
        }

        return ans;
    }
};
```
