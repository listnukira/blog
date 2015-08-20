title: "[LeetCode] Best Time to Buy and Sell Stock III"
date: 2014-10-01 10:51:14
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Dynamic Programming
---
限制在最多兩次的交易內，找出最大的獲利

<!-- more -->

### Solution 1

第一個方法分兩個步驟

1. 先算出從前面到後面每個點的獲利，profitHist 記錄在每個時間點的最大獲利
2. 往回算出最大的獲利

``` c++
class Solution {
public:
    int maxProfit(vector<int> &prices) {
        int len = prices.size(), maxProfit = 0;

        if (len < 2)
            return 0;

        int low = prices[0];
        vector<int> profitsHist(len, 0);
        for (int i = 0; i < len; i++) {
            low = min(low, prices[i]);
            maxProfit = max(maxProfit, prices[i] - low);
            profitsHist[i] = maxProfit;
        }

        int high = prices[len - 1];
        for (int i = len - 1; i >= 0; i--) {
            high = max(high, prices[i]);
            maxProfit = max(maxProfit, high - prices[i] + profitsHist[i]);
        }

        return maxProfit;
    }
};
```

### Solution 2

Discuss 裡看到的 general case solution，適用於各種交易次數，原理待研究

``` c++
class Solution {
public:
    int maxProfit(vector<int> &prices) {
        vector<bool> segs(prices.size());
        int maxProfit = 0;

        if (prices.size() == 0)
            return 0;

        for (int transact = 0; transact < 2; transact++) {
            int i0 = 0, c = 0, cmax = 0;
            vector<int> s;

            for (int i = 0; i < prices.size() - 1; i++) {
                if (i > 0 && segs[i] != segs[i - 1]) {
                    i0 = i;
                    c = 0;
                }

                c = c + prices[i + 1] - prices[i];

                if ((!segs[i] && c <= 0) || (segs[i] && c >=0)) {
                    i0 = i + 1;
                    c = 0;
                }
                else if (cmax < abs(c)) {
                    cmax = abs(c);
                    s = {i0, i};
                }
            }

            if (cmax == 0)
                break;

            for (int i = s[0]; i <= s[1]; i++)
                segs[i] = !segs[i];

            maxProfit += cmax;
        }

        return maxProfit;
    }
};
```
