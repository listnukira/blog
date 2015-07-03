title: "[LeetCode] Roman to Integer"
date: 2014-12-06 15:50:06
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
- Math
---
將羅馬數字轉成整數

<!-- more -->

###Solution

根據 wiki 的介紹，羅馬數字有七個

<pre>
I (1)
V (5)
X (10)
L (50)
C (100)
D (500)
M (1000)
</pre>

根據組合的規則，記錄前一個羅馬數字，如果前一個數字比目前的數字小，就把多加的數字減掉

``` c++
class Solution {
public:
    int romanToInt(string s) {
        unordered_map<char, int> charToInt = {
            {'M', 1000}, {'D', 500}, {'C', 100},
            {'L', 50}, {'X', 10}, {'V', 5},
            {'I', 1}
        };

        int prev = 0, cur = 0;
        int Int = 0;
        for (char c: s) {
            cur = charToInt[c];

            if (cur > prev) {
                Int += (cur - 2 * prev);
            } else {
                Int += cur;
            }

            prev = cur;
        }

        return Int;
    }
};
```
