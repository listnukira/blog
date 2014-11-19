title: "[LeetCode] Generate Parentheses"
date: 2014-09-03 13:48:01
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
- Backtracking
---
給一個數字 n，要產生出所有長度為 2 * n 的合法括號組合

<!-- more -->

###Solution 1

第一個方法比較直覺，一個 ans 陣列存放每一次得到的結果，接著把 ans 裡的每個字串在前面加上 "()"，新增的右括號與右邊循序交換直到最後一個，產生的字串都放入 List 陣列中，接著移除 List 裡重複的字串，清空 ans 並把結果放進去，同複同樣動作直到結束

``` c++
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        ans.push_back("()");

        for (int i = 1; i < n; i++) {

            list<string> strList;
            for (string str : ans) {

                string tmpStr = "()" + str;
                strList.push_back(tmpStr);
                for (int j = 1; j < tmpStr.length() - 1; j++) {
                    swap(tmpStr[j], tmpStr[j + 1]);
                    strList.push_back(tmpStr);
                }

            }

            strList.sort();
            strList.unique();

            ans.clear();
            for (auto&& str : strList) {
                ans.push_back(str);
            }

        }

        return ans;
    }
};
```

###Solution 2

第二個方法是 Discuss 裡看到的解法，覺得蠻漂亮的，所以順便記下來

這個方法會用到兩個堆疊，一個堆疊存字串 s，從 "(" 開始，s 每次會根據條件加入 "(" 或 ")"，另一個堆疊存整數 v，v 代表目前字串已經有幾組合法的括號組合，s 與 v 裡的元素是有對應關係的，所以它們的大小都會是一樣的

每一次執行都會把 s 跟 v 從堆疊裡拿出來，接著分別做以下判斷

* `s.length() == n * 2` 找到一組括號組合，存入 ans 陣列
* `s.length() - v < n` 可以想像成字串長度減掉 v 個合法的右括號，剩下來的左括號數目要是比 n 還少，代表還有空間可以加左括號進去
* `v * 2 < s.length()` 代表可以加入右括號

程式會重複執行直到 s 為空為止

程式碼如下

``` c++
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        stack<string> candidateStack;
        stack<int> validationStack;

        candidateStack.push("(");
        validationStack.push(0);
        while (!candidateStack.empty()) {
            string s = candidateStack.top();
            int v = validationStack.top();
            candidateStack.pop();
            validationStack.pop();

            if (s.length() == n * 2) {
                ans.push_back(s);
                continue;
            }

            if (s.length() - v < n) {
                candidateStack.push(s + "(");
                validationStack.push(v);
            }

            if (v * 2 < s.length()) {
                candidateStack.push(s + ")");
                validationStack.push(v + 1);
            }
        }

        return ans;
    }
};
```
