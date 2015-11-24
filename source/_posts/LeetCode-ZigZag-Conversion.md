title: '[LeetCode] ZigZag Conversion'
date: 2015-11-24 10:50:57
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
---
當字串以鋸齒狀的方式表示時，依序印出每一行的字串

<!-- more -->

以數字 `1 2 3 4 5 6 7 8 9 10 11 12 13`，高度 4 為例

以鋸齒狀方式表示會長得像這樣

<pre>
1           7             13
  2       6   8         12
    3   5       9    11
      4           10
</pre>

所以要印出 `1 7 13 2 6 8 12 3 5 9 11 4 10`

### Solution 1

第一個方法其實有點複雜而且也有點爛，不過都寫了就記錄一下，以上面的例子來說，當高度為 4 的時候，第一行跟最後一行每個數字的間隔都剛好差 `2 * 4 - 2 = 6`，第二行每個數字的間隔分別是 4 和 2，第三行分別是 2 和 4，最後就根據這些規律，依序把每一行的字元加入到字串裡

``` c++
class Solution {
public:
    string convert(string s, int numRows) {
        string str(s);

        if (numRows == 1)
            return s;

        int idx = 0, gap = 2 * numRows - 2;
        for (int row = 0; row < numRows; row++) {
            for (int i = row; i < s.size(); i += gap) {
                str[idx++] = s[i];

                if (row != 0 && row != numRows - 1) {
                    int t = i + gap - (row * 2);
                    if (t < s.size())
                        str[idx++] = s[t];
                }
            }
        }

        return str;
    }
};
```

### Solution 2

第二個方法比較簡單，假設題目給 `numRows = 4`，就準備 4 個字串，每一個字串分別存每一行的字元，把字串裡的字元依序放入這四個字串裡，最後再把四個字串接起來

``` c++
class Solution {
public:
    string convert(string s, int numRows) {
        vector<string> str(numRows);
        int rowIdx = 0, dir = 0;

        if (numRows <= 1)
            return s;

        for (int i = 0; i < s.size(); i++) {
            str[rowIdx].push_back(s[i]);
            
            rowIdx = (dir == 0) ? rowIdx + 1 : rowIdx - 1;
            if (rowIdx == 0) {
                dir = 0;
            } else if (rowIdx == numRows - 1) {
                dir = 1;
            }
        }

        string retStr = "";
        for (auto s : str)
            retStr += s;

        return retStr;
    }
};
```
