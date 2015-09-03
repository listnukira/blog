title: '[LeetCode] Valid Anagram'
date: 2015-09-03 17:28:40
categories: LeetCode
tags:
- LeetCode
- C/C++
- Hash Table
- Sort
---

判斷兩個字串是不是 Anagram (字母可以重新排列成另一個字)

<!-- more -->

兩個字串是 Anagram 代表相同字母的個數會一樣，長度不同一定不是

### Solution 1

第一個方法用 Hash Table 的方式做，字串 s 的字母會在 arr 對應的索引值加一，字串 t 的字母會在 arr 對應的索引值減一，最後 arr 都是零代表字母個數一樣

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        int arr[128] = {};

        if (s.size() != t.size())
            return false;

        for (int i = 0; i < s.size(); i++) {
            arr[s[i]]++;
            arr[t[i]]--;
        }

        for (int i = 97; i < 123; i++) {
            if (arr[i] != 0)
                return false;
        }

        return true;
    }
};
```

### Solution 2

第二個方法用排序，兩個字串分別排序好，如果是 Anagram，則對應索引值的字母都會相同

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.size() != t.size())
            return false;

        sort(s.begin(), s.end());
        sort(t.begin(), t.end());

        for (int i = 0; i < s.size(); i++) {
            if (s[i] != t[i])
                return false;
        }

        return true;
    }
};
```
