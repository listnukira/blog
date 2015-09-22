title: '[LeetCode] First Bad Version'
date: 2015-09-22 16:02:23
categories: LeetCode
tags:
- LeetCode
- C/C++
- Binary Search
toc: false
---
給一個從 1 到 N 的陣列，找出第一個壞的版本數

<!-- more -->

題目要求使用 API 的次數要最少，所以大概只能用二元搜尋來處理，練習二元搜尋的題目

### Solution

```c++
// Forward declaration of isBadVersion API.
bool isBadVersion(int version);

class Solution {
public:
    int firstBadVersion(int n) {
        int start = 1, end = n;

        int mid = (end - start) / 2 + start;
        while (start < end) {
            if (isBadVersion(mid))
                end = mid;
            else
                start= mid + 1;

            mid = (end - start) / 2 + start;
        }

        return mid;
    }
};
```
