title: '[LeetCode] Contains Duplicate'
date: 2015-07-06 13:56:51
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Hash Table
---
判斷陣列裡有沒有重複的元素

<!-- more -->

### Solution

C++ 的 `unordered_set` 在建立的時候會判斷有無重複，重複的就不會再新增了，所以只要判斷建立後的大小是不是跟原本符合，就知道元素有沒有重複

``` c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> map(nums.begin(), nums.end());
        return (map.size() == nums.size()) ? false : true;
    }
};
```
