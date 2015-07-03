title: "[LeetCode] Best Time to Buy and Sell Stock"
date: 2014-09-28 10:36:12
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Dynamic Programming
---
在一次的交易內，算出股票的最大獲利，交易的意思是一買一賣

<!-- more -->

###Solution

在最低點買入最高點賣出就能得到最大的獲利，也就是要找出兩個數字相減，差距最大的
從第一個數字開始，每次都與 minimum 相減，判斷是否超過最大值，如果遇到比 minimum 更小的值就更新 minimum

``` c++
class Solution {
public:
    int maxProfit(vector<int> &prices) {
        int profit = 0, minimum = INT_MAX;

        for (int price: prices) {
            minimum = min(minimum, price);
            profit = max(profit, price - minimum);
        }

        return profit;
    }
};
```
