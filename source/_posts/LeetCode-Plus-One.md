title: "[LeetCode] Plus One"
date: 2014-10-01 18:16:05
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Math
---
模擬位元進位，傳回進位的結果，要從最右邊的位元開始加一

<!-- more -->

### Solution

``` c++
class Solution {
public:
    vector<int> plusOne(vector<int> &digits) {
        vector<int> result;
        vector<int>::iterator it = result.begin();

        int carry = 1;
        for (int i = digits.size() - 1; i >= 0; i--) {
            if (digits[i] + carry == 10) {
                it = result.insert(it, 0);
            } else {
                it = result.insert(it, digits[i] + carry);
                carry = 0;
            }
        }

        if (carry == 1)
            result.insert(it, 1);

        return result;
    }
};
```
