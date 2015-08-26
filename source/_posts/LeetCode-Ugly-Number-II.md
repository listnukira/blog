title: '[LeetCode] Ugly Number II'
date: 2015-08-26 23:19:38
categories: LeetCode
tags:
- LeetCode
- C/C++
- Dynamic Programming
- Heap
- Math
toc: false
---
找出第 N 個 Ugly Number

<!-- more -->

一個 Ugly Number 一定是比較小的 Ugly Number 乘以 `2, 3, 5` 得來的，用陣列來記錄所有的 Ugly Number

假設已經有一個 Ugly Number 陣列為 `1 2 3 4`，則下一個可能的 Ugly Number 有以下這些

乘以 2
`2 4 6 8`

乘以 3
`3 6 9 12`

乘以 5
`5 10 15 20`

下一個 Ugly Number 一定是比 4 大中的數字裡最小的，也就是 5

實際上在計算的時候，不會整個陣列都乘上 `2, 3, 5` 再去找，所以分別用三個索引值來記錄目前乘到哪了

### Solution

```c++
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> uglyNumbers(n);
        int idx2, idx3, idx5, UglyNumber;
        idx2 = idx3 = idx5 = 0;

        uglyNumbers[0] = 1;
        for (int i = 1; i < n; i++) {
            UglyNumber = min(uglyNumbers[idx2] * 2,
                min(uglyNumbers[idx3] * 3, uglyNumbers[idx5] * 5));

            uglyNumbers[i] = UglyNumber;

            if (uglyNumbers[idx2] * 2 == UglyNumber)
                idx2++;
            if (uglyNumbers[idx3] * 3 == UglyNumber)
                idx3++;
            if (uglyNumbers[idx5] * 5 == UglyNumber)
                idx5++;
        }

        return uglyNumbers[n - 1];
    }
};
```
