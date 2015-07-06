title: '[LeetCode] Isomorphic Strings'
date: 2015-07-05 20:18:14
categories: LeetCode
tags:
- LeetCode
- C/C++
- Hash Table
---
判斷兩個字串是否是 Isomorphic，假設字串長度都相同

<!-- more -->

###Solution

用一個 256 大小的陣列當 hash table，key 是字元的 ascii 碼，value 是索引值，如果對應的索引值不同，代表不是 isomorphic，字元重覆出現的話，會更新索引值，索引值最小由 1 開始，因為 hash table 的 value 一開始預設為 0

``` c++
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        int map1[256] = {0};
        int map2[256] = {0};

        for (int i = 0; i < s.size(); i++) {
            if (map1[s[i]] != map2[t[i]])
                return false;

            map1[s[i]] = i + 1;
            map2[t[i]] = i + 1;
        }

        return true;
    }
};
```
