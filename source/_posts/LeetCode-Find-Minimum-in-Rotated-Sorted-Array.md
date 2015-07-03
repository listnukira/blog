title: "[LeetCode] Find Minimum in Rotated Sorted Array"
date: 2015-05-02 14:44:44
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Binary Search
---

給一個排序且被旋轉過的陣列，找出最小值

<!-- more -->

###Solution

這題有點類似 [Find-Peak-Element](/-LeetCode-Find-Peak-Element)，一樣用二分法來找

```c++
class Solution {
public:
    int findMin(vector<int> &num) {
        int left = 0, right = num.size() - 1;

        while (left < right) {
            int mid = left + (right - left) / 2;
            if (num[mid] < num[right])
                right = mid;
            else
                left = mid + 1;
        }

        return num[left];
    }
};
```
