title: "[LeetCode] Valid Palindrome"
date: 2014-11-22 00:06:28
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
- Two Pointers
---
給一個字串，判斷是否迴文，只考慮字母跟數字，忽略大小寫

<!-- more -->

###Solution

從字串的前後比對，遇到字母和數字以外的跳過，如果都沒遇到不一樣的就是迴文

``` c++
class Solution {
public:
    bool isPalindrome(string s) {
        int left = 0, right = s.size() - 1;

        while (left < right) {
            for (; left < right && !isalnum(s[left]); left++);
            for (; left < right && !isalnum(s[right]); right--);

            if (tolower(s[left++]) != tolower(s[right--]))
                return false;
        }

        return true;
    }
};
```
