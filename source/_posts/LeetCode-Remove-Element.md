title: "[LeetCode] Remove Element"
date: 2014-09-19 15:03:17
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Two Pointers
---
從陣列裡刪除指定的值，回傳新陣列的長度

<!-- more -->

### Solution

``` c++
class Solution {
public:
    int removeElement(int A[], int n, int elem) {
        int len = 0;
        for (int i = 0; i < n; i++) {
            if (A[i] != elem)
                A[len++] = A[i];
        }

        return len;
    }
};
```
