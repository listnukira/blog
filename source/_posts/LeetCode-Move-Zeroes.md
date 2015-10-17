title: '[LeetCode] Move Zeroes'
date: 2015-09-28 13:29:03
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Two Pointers
---
將陣列中的零都移到最後

<!-- more -->

分別用兩種方法做，想法差不多，都會用到兩個索引值

### Solution 1

第一個方法把不是零的數字都往前移，剩下的再全部填零

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int nonZeroIdx = 0;

        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != 0)
                nums[nonZeroIdx++] = nums[i];
        }

        for (int i = nonZeroIdx; i < nums.size(); i++)
           nums[i] = 0; 
    }
};
```

### Solution 2

第二個方法少了最後面填零的步驟，直接交換零與非零的數字

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int zeroIdx = 0;

        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != 0)
                swap(nums[i], nums[zeroIdx++]);
        }
    }
};
```
