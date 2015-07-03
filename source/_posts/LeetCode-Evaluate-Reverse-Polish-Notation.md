title: "[LeetCode] Evaluate Reverse Polish Notation"
date: 2014-09-21 15:12:47
categories: LeetCode
tags:
- LeetCode
- C/C++
- Stack
---
算出 Reverse Polish Notation (RPN) 也就是後置式表示法的値

<!-- more -->

###Solution

練習堆疊的題目，遇到數字就放入堆疊，遇到運算子就拿出來運算再放入堆疊，最後堆疊剩下的就是運算結果

``` c++
class Solution {
public:
    int evalRPN(vector<string> &tokens) {
        string operators = "+-*/";
        int val1, val2;
        stack<int> operand;

        for (auto&& str : tokens) {
            if (operators.find(str) != string::npos) {
                val2 = operand.top();
                operand.pop();
                val1 = operand.top();
                operand.pop();

                operand.push(op(str, val1, val2));
            } else {
                operand.push(stoi(str));
            }
        }

        return operand.top();
    }

private:
    int op(string oper, int val1, int val2) {
        if (oper == "+")
            return val1 + val2;

        if (oper == "-")
            return val1 - val2;

        if (oper == "*")
            return val1 * val2;

        if (oper == "/")
            return val1 / val2;
    }
};
```
