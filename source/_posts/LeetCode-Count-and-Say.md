title: "[LeetCode] Count and Say"
date: 2014-10-02 14:42:32
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
---
一 (1)，一個一 (11)，兩個一 (21)，一個二 兩個一 (1211)，一個一 一個二 兩個一 (111211)，三個一 一個二 兩個一 (311221)，每個都是由前面的念法延伸而來，根據這個規律，要找出第 N 個字串

<!-- more -->

### Solution

``` c++
class Solution {
public:
    string countAndSay(int n) {
        string s = "1";

        if (n == 0)
            return "";

        for (int i = 1; i < n; i++) {
            string tmp = "";
            char val = s[0];
            int cnt = 1;

            for (int j = 1; j < s.length(); j++) {
                if (s[j] == val) {
                    cnt++;
                    continue;
                }

                tmp += to_string(cnt) + val;
                val = s[j];
                cnt = 1;
            }

            tmp += to_string(cnt) + val;
            s = tmp;
        }

        return s;
    }
};
```
