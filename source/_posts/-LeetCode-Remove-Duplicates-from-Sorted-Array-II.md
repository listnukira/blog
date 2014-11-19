title: "[LeetCode] Remove Duplicates from Sorted Array II"
date: 2014-09-04 17:50:10
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Two Pointers
---
[Remove Duplicates from Sorted Array](/2014/09/04/-LeetCode-Remove-Duplicates-from-Sorted-Array/) 的進階版，現在同一個數字可以允許重複兩次，把重複兩次以上的整數刪掉，並回傳新的陣列跟陣列長度，不能用到額外的陣列

<!-- more -->

###Solution

多用一個變數 repeat 存數字的重複次數，當 repeat 值大於 1 時跳過重複的數字，遇到不同數字時把 repeat 設為 0

``` c++
class Solution {
public:
    int removeDuplicates(int A[], int n) {
        int val = 0, len = 0, repeat = 0;
        for (int i = 0; i < n; i++) {

            if (len == 0 || (val ^ A[i]) != 0) {
                A[len++] = val = A[i];
                repeat = 0;
                continue;
            }

            if (++repeat == 1) {
                A[len++] = A[i];
            }
        }

        return len;
    }
};
```
