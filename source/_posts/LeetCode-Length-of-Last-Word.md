title: "[LeetCode] Length of Last Word"
date: 2014-10-06 15:13:43
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
---
計算字串裡最後一個字的長度

<!-- more -->

### Solution

``` c++
class Solution {
public:
    int lengthOfLastWord(const char *s) {
        int length = 0;

        while (*s != '\0') {
            if (*s++ != ' ') {
                length++;
            } else if (*s && *s != ' ') {
                length = 0;
            }
        }

        return length;
    }
};
```
