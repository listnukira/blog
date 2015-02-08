title: "[LeetCode] Excel Sheet Column Number"
date: 2015-02-01 01:28:55
categories: LeetCode
tags:
- LeetCode
- C/C++
- Math
---
給 Excel Sheet Title，傳回對應的列數

<!-- more -->

與 [Excel Sheet Column Title](/-LeetCode-Excel-Sheet-Column-Title/) 相反的問題

###Solution

``` c++
class Solution {
public:
    int titleToNumber(string s) {
        int number = 0;

        for (int i = 0; i < s.size(); i++)
            number = number * 26 + (s[i] - 'A' + 1);

        return number;
    }
};
```
