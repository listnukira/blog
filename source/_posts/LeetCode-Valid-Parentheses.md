title: "[LeetCode] Valid Parentheses"
date: 2014-08-29 15:19:22
categories: LeetCode
tags:
- LeetCode
- C/C++
- Stack
- String
---
判斷輸入的字串是否由成對的括號組成

<!-- more -->

###Solution

將所有遇到的左括號都放進堆疊裡，遇到右括號就跟堆疊頂比較，成對就把左括號從堆疊移除，最後堆疊沒東西就代表示都是成對的

``` c++
class Solution {
public:
    map<char, char> parentthesesMap;

    Solution() {
        parentthesesMap[')'] = '(';
        parentthesesMap[']'] = '[';
        parentthesesMap['}'] = '{';
    }

    bool isValid(string s) {
        stack<char> stk;

        for (auto&& ch : s) {
            if (ch == '(' || ch == '[' || ch == '{') {
                stk.push(ch);
            } else if (ch == ')' || ch == ']' || ch == '}') {
                if (!stk.empty() && stk.top() == parentthesesMap[ch])
                    stk.pop();
                else
                    return false;
            } else {}
        }

        return stk.empty() ? true : false;
    }
};
```
