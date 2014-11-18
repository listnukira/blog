title: "[LeetCode] Word Break II"
date: 2014-08-27 10:25:41
categories: LeetCode
tags:
- LeetCode
- C/C++
- Dynamic Programming
- Backtracking
---
Word Break 的延伸，這次要找出所有可能的組合，但是要注意還是有可能出現無法組合的例子

<!-- more -->

###Solution

首先先判斷題目所給的字串是否可以由 dict 所組成，接下來遞迴尋找可能的字串

遞迴首先會分成左右兩個字串，當左邊的字串可以由 dict 所組成，則把右邊的字串當成參數繼續執行遞迴，並把結果與左邊的字串合併，最後回傳的就是全部的組合

``` c++
class Solution {
public:
    vector<string> recursive(string s, unordered_set<string> &dict)
    {
        string rightStr, leftStr;
        vector<string> ret;
        int len = s.length();

        if (dict.find(s) != dict.end())
            ret.push_back(s);

        for(int i = 1; i < len; i++) {
            leftStr = s.substr(0, i);
            rightStr = s.substr(i, len - i);

            if (dict.find(leftStr) != dict.end()) {
                vector<string> recRet = recursive(rightStr, dict);
                for (int j = 0; j < recRet.size(); j++) {
                    ret.push_back(leftStr + " " + recRet[j]);
                }
            }
        }

        return ret;
    }

    vector<string> wordBreak(string s, unordered_set<string> &dict) {
        int len = s.size();
        vector<bool> canSegment(len + 1, false);
        vector<string> ans;

        canSegment[0] = true;
        for (int i = 1; i < len + 1; i++) {
            for (int j = 0; j < i; j++) {
                unordered_set<string>::const_iterator it = dict.find(s.substr(j, i - j));
                if (canSegment[j] == true && it != dict.end()) {
                    canSegment[i] = true;
                    break;
                }
            }
        }

        if (canSegment[len] == true)
            ans = recursive(s, dict);

        return ans;
    }
};
```
