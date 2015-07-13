title: '[LeetCode] Restore IP Addresses'
date: 2015-07-06 14:55:00
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
- Backtracking
---
給一個由數字組成的字串，傳回所有可能的 IP 位址

<!-- more -->

合法的 IP 位址，要有四個數字，每個數字不能大於 255，除了 0 以外，其它數字不能以 0 開頭

###Solution 1

第一個方法用 3 個 for 迴圈找出四個數字，分別判斷個別的數字是不是合法的

``` c++
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
        vector<string> validIP;

        for (int i = 1; i <= 3 && i < s.size(); i++) {
            for (int j = 1; j <= 3 && i + j < s.size(); j++) {
                for (int k = 1; k <= 3 && i + j + k < s.size(); k++) {
                    string A(s, 0, i);
                    string B(s, i, j);
                    string C(s, i + j, k);
                    string D(s, i + j + k);
                    if (isValid(A) && isValid(B) && isValid(C) && isValid(D))
                        validIP.push_back(A + "." + B + "." + C + "." + D);
                }
            }
        }

        return validIP;
    }
private:
    bool isValid(string s) {
        if (s.size() > 3 || (s[0] == '0' && s.size() > 1) || stoi(s) > 255)
            return false;

        return true;
    }
};
```

###Solution 2

第二個方法改成用遞迴的方式找，主要的判斷都跟第一個方法差不多

``` c++
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
        vector<string> validIP;
        vector<int> candidate;
        if (s.size() < 4 || s.size() > 12)
            return validIP;

        restoreIPRecur(s, validIP, candidate, 0);
        return validIP;
    }

    void restoreIPRecur(string s, vector<string> &validIP, vector<int> &candidate, int pos) {
        if (candidate.size() == 4 && pos == s.size()) {
            validIP.push_back(to_string(candidate[0]) + "." +
                              to_string(candidate[1]) + "." +
                              to_string(candidate[2]) + "." +
                              to_string(candidate[3]));

            return;
        }

        if (candidate.size() == 3 && s.size() - pos > 3)
            return;

        for (int i = 1; i <= 3; i++) {
            if (s[pos] == '0' && i > 1)
                return;

            if (pos + i > s.size())
                return;

            int value = stoi(s.substr(pos, i));
            if (value > 255)
                return;

            candidate.push_back(value);
            restoreIPRecur(s, validIP, candidate, pos + i);
            candidate.pop_back();
        }
    }
};
```
