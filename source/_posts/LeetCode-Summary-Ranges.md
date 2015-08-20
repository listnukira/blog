title: '[LeetCode] Summary Ranges'
date: 2015-07-16 23:18:31
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
---
給一個排序好且沒有重複的整數陣列，傳回各個區間的字串

<!-- more -->

給 `[0,1,2,4,5,7]` 會傳回 `["0->2","4->5", "7"]`

### Solution

將第一個數字記錄起來並放到 vector 裡，接下來只要判斷每個數字是不是前面的數字加一，如果是的話就把 vector 最後的區間字串刪掉然後更新，不是的話代表前面的區間已經結束，將現在的數字存為新的字串並記錄區間的開始值

``` c++
class Solution {
public:
    vector<string> summaryRanges(vector<int>& nums) {
        vector<string> ranges;
        int start;

        for (int i = 0; i < nums.size(); i++) {
            if (i > 0 && nums[i - 1] + 1 == nums[i]) {
                ranges.pop_back();
                ranges.push_back(to_string(start) + "->" + to_string(nums[i]));
            } else {
                start = nums[i];
                ranges.push_back(to_string(nums[i]));
            }
        }

        return ranges;
    }
};
```
