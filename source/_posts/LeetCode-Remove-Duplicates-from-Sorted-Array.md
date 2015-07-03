title: "[LeetCode] Remove Duplicates from Sorted Array"
date: 2014-09-04 15:24:08
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Two Pointers
---
給一個已經排序好的整數陣列，把重複的整數刪到只剩一個，並回傳新的陣列跟陣列長度，不能用到額外的陣列

<!-- more -->

###Solution

從頭開始重新指定陣列的值，len 記錄目前的長度，遇到重複的就跳過

``` c++
class Solution {
public:
    int removeDuplicates(int A[], int n) {
        int len = 0;

        for (int i = 0; i < n; i++) {
            if (len == 0 || (A[len - 1] ^ A[i]) != 0) {
                A[len++] = A[i];
            }
        }

        return len;
    }
};
```
