title: '[LeetCode] Jewels and Stones'
categories: LeetCode
tags:
  - LeetCode
  - C/C++
  - Hash Table
date: 2018-09-01 15:49:08
---
給兩個字串 J 跟 S，字串 J 裡面的字母不會重覆，要計算出每個在 J 裡面的字母在 S 裡出現的次數總和


<!-- more -->

### Solution 1

最簡單的方法，一個一個比對

``` c
int numJewelsInStones(char* J, char* S) {
    int count = 0;

    for (int i = 0; i < strlen(J); i++) {
        for (int j = 0; j < strlen(S); j++) {
            if (J[i] == S[j])
                count++;
        }
    }

    return count;
}
```

### Solution 2

先建立好 ASCII table，如果字元在 J 裡有出現就設成 1，接著用 table 來檢查字元是否有在 S 裡面出現，會比第一個方法稍微快些

``` c
int numJewelsInStones(char* J, char* S) {
    int count = 0;
    char s[128] = {0};

    for (int i = 0; i < strlen(J); i++) {
        s[(int)J[i]] = 1;
    }

    for (int j = 0; j < strlen(S); j++) {
        if (s[(int)S[j]])
            count++;
    }

    return count;
}
```
