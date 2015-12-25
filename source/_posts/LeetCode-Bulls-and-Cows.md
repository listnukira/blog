title: '[LeetCode] Bulls and Cows'
date: 2015-12-11 22:36:40
categories: LeetCode
tags:
- LeetCode
- C/C++
- Hash Table
toc: false
---
猜數字，要傳回幾 A 幾 B

<!-- more -->

### Solution

用一個大小為 10 的整數陣列 map 紀錄每個數字出現的情況，一開始初始為零，secret 有出現的數字就會在 map 對應的地方加一，guess 則是減一，變數 A 代表數字跟位置都對的個數，B 代表數字對但位置不對的個數

因為 secret 與 guess 的長度會相同，所以依序比對相對應的數字，當對應的數字一樣時，變數 A 就加一，數字不一樣時，map 就根據 secret 與 guess 的值來執行加一減一的動作，secret 的話加一，guess 減一，secret 加一前會先判斷 map 裡的值是不是小於零，小於零代表 guess 把值減過了，也就是有猜過了，這時 B 就要加一，guess 減一前也要做同樣的動作，只是是看值有沒有大於零

```c++
class Solution {
public:
    string getHint(string secret, string guess) {
        int map[10] = {0};
        int A = 0, B = 0;

        for (int i = 0; i < secret.size(); i++) {
            if (secret[i] == guess[i]) {
                A++;
            } else {
                if (map[secret[i] - '0']++ < 0)
                    B++;
                if (map[guess[i] - '0']-- > 0)
                    B++;
            }
        }

        return to_string(A) + "A" + to_string(B) + "B";
    }
};
```
