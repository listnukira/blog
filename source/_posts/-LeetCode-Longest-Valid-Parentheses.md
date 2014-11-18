title: "[LeetCode] Longest Valid Parentheses"
date: 2014-09-01 16:03:56
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
- Dynamic Programming
---
找出所有合法括號組合中，最長的長度

<!-- more -->

###Solution

在解 Valid Parentheses 時，堆疊裡存的是左括號，遇到右括號就 pop，最後以堆疊是否為空來判斷是不是合法的括號組合

而這個題目需要的是最長的合法括號組合，所以堆疊改存左括號的 index，每當遇到右括號就先 pop，接著以右括號的 index 減掉堆疊頂的 index 值，會得到長度，但是如果遇到像 `()` 這樣，pop 之後堆疊會是空的，所以需要另外一個變數 rIdx 記錄這組合法括號的起始位置，初始值為 -1

重點大致如下
遇到左括號，將左括號的 index 放入堆疊
遇到右括號，堆疊為空，更新 rIdx 為右括號的 index
遇到右括號，堆疊裡有東西，pop 之後堆疊不為空，長度的算法是 `index - stack.top()`
遇到右括號，堆疊裡有東西，pop 之後堆疊為空，長度的算法是 `index - rIdx`

以 `(()(()()` 為例

``` bash
0 1 2 3 4 5 6 7
( ( ) ( ( ) ( )
```

index = 0，`s[0] = '('`，將 0 放進堆疊
index = 1，`s[1] = '('`，將 1 放進堆疊
index = 2，`s[2] = ')'`，pop 後堆疊頂存的 index 是 0，長度為 `2 - 0 = 2`
index = 3，`s[3] = '('`，將 3 放進堆疊
index = 4，`s[4] = '('`，將 4 放進堆疊
index = 5，`s[5] = ')'`，pop 後堆疊頂存的 index 是 3，長度為 `5 - 3 = 2`
index = 6，`s[6] = '('`，將 6 放進堆疊
index = 7，`s[7] = ')'`，pop 後堆疊頂存的 index 是 3，長度為 `7 - 3 = 4`

另一個例子 `))()(()`

``` bash
0 1 2 3 4 5 6
) ) ( ) ( ( )
```

index = 0，`s[0] = ')'`，更新 rIdx，`rIdx = 0`
index = 1，`s[1] = ')'`，更新 rIdx，`rIdx = 1`
index = 2，`s[2] = '('`，將 2 放進堆疊
index = 3，`s[3] = ')'`，pop 後堆疊為空，長度為 `3 - 1 = 2`
index = 4，`s[4] = '('`，將 4 放進堆疊
index = 5，`s[5] = '('`，將 5 放進堆疊
index = 6，`s[6] = ')'`，pop 後堆疊頂存的 index 是 4，長度為 `6 - 4 = 2`

程式碼如下

``` c++
class Solution {
public:

    int longestValidParentheses(string s) {
        stack<int> stk;
        int ansMax = 0, rIdx = -1;

        for (int i = 0; i < s.length(); i++) {
            if (s[i] == '(') {
                stk.push(i);
            } else {
                if (!stk.empty()) {
                    stk.pop();
                    ansMax = max(ansMax, i - (stk.empty() ? rIdx : stk.top()));
                } else {
                    rIdx = i;
                }
            }
        }

        return ansMax;
    }
};
```
