title: "[LeetCode] Search in Rotated Sorted Array II"
date: 2014-10-05 20:47:12
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Binary Search
---
[Search in Rotated Sorted Array](/-LeetCode-Search-in-Rotated-Sorted-Array/) 的延伸，這次排序好的陣列裡可以有重複的數字，要判斷 target 是否在陣列裡

<!-- more -->

###Solution

因為會有重複的數字，所以必須多處理一種情況，當 `A[left] == A[middle]` 時，`left++` 再重新判斷，其它的處理跟原本一樣
當重複的數字越多，時間複雜度會從 O(logN)上升到 O(N)

``` c++
class Solution {
public:
    bool search(int A[], int n, int target) {
        int left = 0, right = n - 1;

        while (left <= right) {
            int middle = (left + right) / 2;

            if (A[middle] == target)
                return true;

            if (A[left] < A[middle]) {
                if (target >= A[left] && target <= A[middle]) {
                    right = middle - 1;
                } else {
                    left = middle + 1;
                }
            } else if (A[left] > A[middle]) {
                if (target >= A[middle] && target <= A[right]) {
                    left = middle + 1;
                } else {
                    right = middle - 1;
                }
            } else {
                left++;
            }
        }

        return false;
    }
};
```
