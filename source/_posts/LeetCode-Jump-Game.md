title: "[LeetCode] Jump Game"
date: 2014-10-15 20:55:30
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Greedy
---
給一個正整數陣列，每個數字代表可以往後走幾步，判斷能否從第一個數走到最後一個

<!-- more -->

### Solution

step 記錄剩下的步數，每走一步就更新能走的步數
走到倒數第二個數字如果 setp 大於 0 代表可以走到最後

``` c++
class Solution {
public:
    bool canJump(int A[], int n) {
        int step = A[0];
        for (int i = 1; i < n - 1 && step > 0; i++)
            step = max(step - 1, A[i]);

        return (step > 0 || n == 1) ? true : false;
    }
};
```
