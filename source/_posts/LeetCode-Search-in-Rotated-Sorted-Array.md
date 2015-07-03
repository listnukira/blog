title: "[LeetCode] Search in Rotated Sorted Array"
date: 2014-10-05 15:46:50
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Binary Search
---
給一個排序過並且平移過的陣列，陣列沒有重複的數字，要找出陣列裡的某數字

<!-- more -->

###Solution

因為陣列經過平移，所以沒有辦法直接用 binary search，而經過平移的陣列，左半邊或右半邊會是正常排序的順序，這時可以用已排序好的那邊判斷 target 是否在裡面，藉此更新搜尋的範圍

``` c++
class Solution {
public:
    int search(int A[], int n, int target) {
        int left = 0, right = n - 1;

        while (left <= right) {
            int middle = (left + right) / 2;

            if (A[middle] == target)
                return middle;

            if (A[left] <= A[middle]) {
                if (target >= A[left] && target <= A[middle]) {
                    right = middle - 1;
                } else {
                    left = middle + 1;
                }
            } else {
                if (target >= A[middle] && target <= A[right]) {
                    left = middle + 1;
                } else {
                    right = middle - 1;
                }
            }
        }

        return -1;
    }
};
```
