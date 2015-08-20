title: "[LeetCode] Unique Binary Search Trees"
date: 2015-01-06 17:27:28
categories: LeetCode
tags:
- LeetCode
- C/C++
- Tree
- Dynamic Programming
---
算出 N 個節點共有多少種不同組合的二元樹

<!-- more -->

### Solution

假設總共有 4 個點，一個固定為根節點，則所有的組合方式由剩下 3 個節點決定，計算方式如下

`Total = L0 * R3 + L1 * R2 + L2 * R1 + L3 * R0`

L0 代表左邊沒有任何節點，R3 代表右邊有 3 個節點時，不同組合的二元樹數量，同時用一個表 DP 來記錄 N 個節點時的結果

``` c++
class Solution {
public:
    int numTrees(int n) {
        vector<int> DP(n + 1, 1);

        for (int i = 2; i <= n; i++) {
            int treeCount = 0;
            for (int nodeNumL = 0; nodeNumL < i; nodeNumL++) {
                int nodeNumR = i - 1 - nodeNumL;
                treeCount += DP[nodeNumL] * DP[nodeNumR];
            }

            DP[i] = treeCount;
        }

        return DP[n];
    }
};
```
