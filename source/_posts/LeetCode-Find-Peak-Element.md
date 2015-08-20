title: "[LeetCode] Find Peak Element"
date: 2015-05-01 10:39:11
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Binary Search
---

找出陣列裡區間的最大值，任意區間裡的都可以

<!-- more -->

### Solution 1

第一個方法從陣列第二個元素開始，只要目前的這個數字比前面的數字還小，那前面的數字就是區間的最大值，時間複雜度是 O(N)

```c++
class Solution {
public:
    int findPeakElement(const vector<int> &num) {
        for (int i = 1; i < num.size(); i++) {
            if (num[i] < num[i - 1])
                return i - 1;
        }

        return num.size() - 1;
    }
};
```

### Solution 2

第二個方法用二分法來找，每次都往大的地方走，時間複雜度應該是 O(logN)

```c++
class Solution {
public:
    int findPeakElement(const vector<int> &num) {
        int left = 0;
        int right = num.size() - 1;

        while (left < right) {
            int mid = left + (right - left) / 2;
            if (num[mid] > num[mid + 1])
                right = mid;
            else
                left = mid + 1;
        }

        return left;
    }
};
```
