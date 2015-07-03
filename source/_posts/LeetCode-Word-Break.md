title: "[LeetCode] Word Break"
date: 2014-08-27 00:09:31
categories: LeetCode
tags:
- LeetCode
- C/C++
- Dynamic Programming
---
給一個字串 s 和由許多字串組成的字典檔 dict，要判斷 s 是否可以由字典檔裡的字串組合而成

<!-- more -->

###Solution

用遞迴的方式去解可能會超時，所以改用 DP 的方式寫，建立陣列 canSegment，為了程式碼簡潔，canSegment 的大小為字串長度加一，並且把初始條件 canSegment[0] 設定為 true，接下來由字串的第一個字元開始判斷符不符合條件

用以下例子來說明

```
s = "regulartest"
dict = ["re", "gu", "lartest"]

canSegment[0] 是初始條件，設定為 true
canSegment[1] 代表 "r" 可否由 dict 組成
canSegment[2] 代表 "re"
canSegment[3] 代表 "reg"
　　　˙
　　　˙
　　　˙
canSegment[11] 代表 "regulartest"

這個例子裡，有三個值會被設為 true，分別是
canSegment[2] "re", canSegment[4] "regu", canSegment[11] "regulartest"
```

程式碼如下

``` c++
class Solution {
public:
    bool wordBreak(string s, unordered_set<string> &dict) {
        int len = s.length();
        vector<bool> canSegment(len + 1, false);

        canSegment[0] = true;
        for (int i = 1; i < len + 1; i++) {
            for (int j = 0; j < i; j++) {
                if (canSegment[j] && dict.find(s.substr(j, i - j)) != dict.end()) {
                    canSegment[i] = true;
                    break;
                }
            }
        }

        return canSegment[len];
    }
};
```
