title: '[LeetCode] Reverse String'
date: 2016-08-11 15:00:07
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
- Two Pointers
toc: false
---
字串反轉，將 "hello" 轉成 "olleh"

<!-- more -->

### Solution

```c++
class Solution {
public:
    string reverseString(string s) {
        int len = s.length();
        for (int i = 0; i < len / 2; i++)
            swap(s[i], s[len - 1 - i]);

        return s;
    }
};
```
