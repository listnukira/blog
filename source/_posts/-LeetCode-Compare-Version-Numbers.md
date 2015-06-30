title: "[LeetCode] Compare Version Numbers"
date: 2015-03-21 22:35:40
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
---
比較兩個以字串顯示的版本號碼，版本號碼只會出現數字還有小數點

<!-- more -->

###Solution

原本以為只會有這種像`13.37`這種型式的版本號，後來發現版本號可能很長，所以用函式`splitVersion`分離版本號的數字，再來比對相對應的數字

``` c++
class Solution {
public:
    int compareVersion(string version1, string version2) {
        vector<int> v1, v2;

        splitVersion(version1, v1);
        splitVersion(version2, v2);

        for (int i = 0, j = 0; i < v1.size() || j < v2.size(); i++, j++) {
            int ver1 = (i < v1.size()) ? v1[i] : 0;
            int ver2 = (j < v2.size()) ? v2[j] : 0;

            if (ver1 - ver2 != 0)
                return (ver1 > ver2) ? 1 : -1;
        }

        return 0;
    }
private:
    void splitVersion(string version, vector<int>& v) {
        int idx = 0;
        size_t found;

        while ((found = version.find(".", idx)) != string::npos) {
            v.push_back(stoi(version.substr(idx, found - idx)));
            idx = found + 1;
        }

        v.push_back(stoi(version.substr(idx)));
    }
};
```
