title: "[LeetCode] Implement strStr()"
date: 2014-12-07 15:15:26
categories: LeetCode
tags:
- LeetCode
- C/C++
- String
- Two Pointers
---
實作字串的搜尋功能

<!-- more -->

### Solution 1

第一個方法實作 Knuth-Morris-Pratt algorithm，也就是 KMP 演算法，重點在於 failure function 的了解與計算

更詳細的介紹就參考 [字符串匹配的KMP算法](http://www.ruanyifeng.com/blog/2013/05/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm.html) 和 [Knuth-Morris-Pratt algorithm](http://www-igm.univ-mlv.fr/~lecroq/string/node8.html#SECTION0080)，這兩篇文章有很清楚的解釋

``` c++
class Solution {
public:
    int strStr(char *haystack, char *needle) {
        int lenS = strlen(haystack), lenP = strlen(needle);
        int idxS = 0, idxP = 0;
        int *failure = new int[lenP];

        failureFunction(needle, lenP, failure);

        while (idxS < lenS && idxP < lenP) {
            if (haystack[idxS] == needle[idxP]) {
                idxS++;
                idxP++;
            } else {
                if (idxP == 0)
                    idxS++;
                else
                    idxP = failure[idxP - 1];
            }
        }

        delete [] failure;
        return (idxP < lenP) ? -1 : idxS - lenP;
    }
private:
    void failureFunction(char *s, int len, int failure[]) {
        failure[0] = 0;

        int i = 1, j = 0;
        while (i < len) {
            if (s[i] == s[j]) {
               failure[i] = j + 1;
               i++;
               j++;
            } else if (j > 0) {
                j = failure[j - 1];
            } else {
                failure[i] = 0;
                i++;
            }
        }
    }
};
```
