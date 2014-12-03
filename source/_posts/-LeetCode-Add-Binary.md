title: "[LeetCode] Add Binary"
date: 2014-11-26 23:53:54
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
- Math
---
給兩個以字串表示的 binary，算出兩個字串的和

<!-- more -->

###Solution 1

第一個方法就是硬幹，把比較短的那個字串前面補 0，補到兩個字串長度一樣，接著再從最後一個字元開始相加

``` c++
class Solution {
public:
    string addBinary(string a, string b) {
        int aLen = a.size(), bLen = b.size();
        int idx = max(aLen - 1, bLen - 1);
        int maxLen = max(aLen, bLen);
        
        for (int i = 0; i < maxLen - aLen; i++)
            a = "0" + a;

        for (int i = 0; i < maxLen - bLen; i++)
            b = "0" + b;

        string sum = "";
        bool carry = false;
        while (idx >= 0) {
            if (a[idx] == b[idx] && a[idx] == '1') {
                if (carry)
                    sum = "1" + sum;
                else
                    sum = "0" + sum;

                carry = true;
            } else if (a[idx] != b[idx]) {
                if (carry)
                    sum = "0" + sum;
                else
                    sum = "1" + sum;
            } else {
                if (carry)
                    sum = "1" + sum;
                else
                    sum = "0" + sum;

                carry = false;
            }

            idx--;
        }
        
        if (carry)
            sum = "1" + sum;

        return sum;
    }
};
```

###Solution 2

第一個方法的改進版，把字串的每個位元轉成數字，用 XOR 做運算

``` c++
class Solution {
public:
    string addBinary(string a, string b) {
        string sum = "";
        int aIdx = a.size() - 1, bIdx = b.size() - 1;
        int aDigit, bDigit, carry = 0;

        while (aIdx >= 0 || bIdx >= 0 || carry == 1) {
            aDigit = (aIdx-- >= 0) ? a[aIdx + 1] - '0' : 0;
            bDigit = (bIdx-- >= 0) ? b[bIdx + 1] - '0' : 0;

            sum = static_cast<char> ((aDigit ^ bDigit ^ carry) + '0') + sum;
            carry = (aDigit + bDigit + carry > 1) ? 1 : 0;
        }

        return sum;
    }
};
```
