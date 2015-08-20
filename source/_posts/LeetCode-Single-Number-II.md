title: "[LeetCode] Single Number II"
date: 2014-08-26 18:00:58
categories: LeetCode
tags:
- LeetCode
- C/C++
- Bit Manipulation
---
Single Number 的進階版，現在每個數字會出現三次，只有一個數字會出現一次，同樣要在線性時間內並且沒用到額外記憶體的情況下找出這個數字

<!-- more -->

### Solution

主要想法是模擬二進位的運算，將每個數字想像成由二進位表示，由於資料形態是整數，所以會有 32 個位元，變數 one，two，three，分別記錄每個位元出現的次數

從第一個數字開始，首先找出 A[i] 與 one 有那些位元重疊，會重疊代表這些位元出現兩次

`A[i] & one`

出現兩次的記錄在 two 變數裡

`two |= A[i] & one`

接下來執行 XOR 運算，把出現兩次位元會清成 0

`one ^= A[i]`

one 與 two 都出現的位元代表出現三次

`three = one & two`

已經把出現三次的存在 three 裡了，所以把 one 跟 two 的清掉
`one &= ~three`
`two &= ~three`

最後 one 的值就是只出現一次的數字了

``` c++
class Solution {
public:
    int singleNumber(int A[], int n) {
        int one = 0, two = 0, three = 0;

        for (int i = 0; i < n; i++) {
            two |= A[i] & one;
            one ^= A[i];
            three = one & two;
            one &= ~three;
            two &= ~three;
        }

        return one;
    }
}
```
