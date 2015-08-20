title: '[LeetCode] Contains Duplicate II'
date: 2015-07-06 14:27:47
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Hash Table
---
判斷陣列裡是否有重複元素之間的距離少於 k

<!-- more -->

### Solution

用 `map` 紀錄元素(key)與索引值(index)的對應關係，每次都將元素新增進 `map`

`p.second == false` 代表有重複的元素
`p.first->second` 代表已存在元素的索引值

如果元素有重複，索引值相減判斷是否有超過 k
最後需要更新元素最新的索引值

``` c++
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        unordered_map<int, int> map;

        for (int i = 0; i < nums.size(); i++) {
            pair<unordered_map<int, int>::iterator, bool> p = map.insert({nums[i], i});

            if (p.second == false && i - p.first->second <= k)
                return true;

            p.first->second = i;
        }

        return false;
    }
};
```
