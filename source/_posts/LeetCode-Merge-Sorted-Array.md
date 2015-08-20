title: "[LeetCode] Merge Sorted Array"
date: 2014-12-02 17:45:53
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Two Pointers
---
把兩個排序好的陣列合併到第一個陣列

<!-- more -->

### Solution

陣列都已經排序好了，而第一個陣列的後面都是空的，所以新的陣列由第一個陣列後面開始排序

``` c++
class Solution {
public:
    void merge(int A[], int m, int B[], int n) {
        int aIdx = m - 1, bIdx = n - 1;
        int idx = m + n - 1;

        while (bIdx >= 0) {
            if (aIdx >= 0)
                A[idx--] = (A[aIdx] > B[bIdx]) ? A[aIdx--] : B[bIdx--];
            else
                A[idx--] = B[bIdx--];
        }
    }
};
```
