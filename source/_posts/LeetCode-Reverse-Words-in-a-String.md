title: "[LeetCode] Reverse Words in a String"
date: 2014-09-21 15:31:10
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
---
給一個字串，反轉字串裡的單字，反轉後的字串前後不能有空白，字的間隔只能有一個空白

<!-- more -->

### Solution

用 C++ 的 stringstream 可以很簡單的處理

``` c++
class Solution {
public:
    void reverseWords(string &s) {
        istringstream istream(s);
        s = "";

        string word;
        while (istream >> word) {
            s = word + " " + s;
        }
        s = s.substr(0, s.length() - 1);
    }
};
```
