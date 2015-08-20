title: "[LeetCode] Longest Common Prefix"
date: 2014-12-03 18:00:28
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
---
找出字串陣列裡全部字串的 Longest Common Prefix

<!-- more -->

### Solution

以第一個字串為基礎，慢慢增加字串的長度，接著跟後面所有的字串比較

``` c++
class Solution {
public:
    string longestCommonPrefix(vector<string> &strs) {
        if (strs.size() == 0)
            return "";

        string s;
        for (int i = 0; i < strs[0].size(); i++) {
            s = strs[0].substr(0, i + 1);

            for (string str: strs) {
                if (str.compare(0, i + 1, s) != 0)
                    return strs[0].substr(0, i);
            }
        }

        return s;
    }
};
```
