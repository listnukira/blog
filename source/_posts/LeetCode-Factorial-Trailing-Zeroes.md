title: "[LeetCode] Factorial Trailing Zeroes"
date: 2015-03-12 23:12:18
categories: LeetCode
tags:
- LeetCode
- C/C++
- Math
---
計算 n! 後面總共有多少個零

<!-- more -->

### Solution

一個數字乘以 10 就會多一個零，所以要找出 n! 總共乘了幾次 10，而 `10 = 2 * 5`，在連乘的過程中，2 的出現次數一定比 5 還要多，所以最後題目變成總共乘了幾次 5

`zeros = (n / 5) + (n / 25) + (n / 125) + ...`

``` c++
class Solution {
public:
    int trailingZeroes(int n) {
        int zeros = 0;

        for (unsigned long i = 5; i <= n; i *= 5)
            zeros += (n / i);

        return zeros;
    }
};
```
