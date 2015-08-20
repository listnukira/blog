title: "[LeetCode] Best Time to Buy and Sell Stock II"
date: 2014-09-29 10:43:51
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Greedy
---
不限制買賣的次數，也是要找出最大的獲利

<!-- more -->

### Solution

因為不限制買賣次數，所以只要每次都買在低點賣在高點，就能有會大的獲利，也就是把每一段上升的差值都加起來

``` c++
class Solution {
public:
    int maxProfit(vector<int> &prices) {
        int len = prices.size();
        int totalProfit = 0;

        for (int i = 0; i < len - 1; i++) {
            if (prices[i + 1] > prices[i])
                totalProfit += prices[i + 1] - prices[i];
        }

        return totalProfit;
    }
};
```
