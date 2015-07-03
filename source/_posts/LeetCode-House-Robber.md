title: "[LeetCode] House Robber"
date: 2015-05-02 12:11:30
categories: LeetCode
tags:
- LeetCode
- C/C++
- Dynamic Programming
---

找出陣列裡所有數字加起來的最大值，數字間不能相鄰

<!-- more -->

###Solution

用來練習 DP 的題目，用 Bottom up 的方式來建 table

第 i 項可以由 `table[i - 2] + num[i]` 或 `table[i - 1]` 而來，公式如下

`table[i] = max(table[i - 2] + num[i], table[i - 1])`

```c++
class Solution {
public:
    int rob(vector<int> &num) {
        int n = num.size();
        vector<int> table(n);

        if (n < 2)
            return (n == 0) ? 0 : num[0];

        table[0] = num[0];
        table[1] = max(num[0], num[1]);
        for (int i = 2; i < n; i++)
            table[i] = max(table[i - 2] + num[i], table[i - 1]);

        return table[n - 1];
    }
};
```
