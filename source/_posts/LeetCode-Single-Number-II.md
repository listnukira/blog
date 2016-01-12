title: "[LeetCode] Single Number II"
date: 2014-08-26 18:00:58
categories: LeetCode
tags:
- LeetCode
- C/C++
- Bit Manipulation
---
給一個整數陣列，每個數字都會出現三次，只有一個數字會出現一次，要在 O(n) 時間，O(1) 空間的情況下找出只出現一次的數字

<!-- more -->

[Single Number](/LeetCode-Single-Number) 的進階版

### Solution 1

每個數字由二進位 32 個位元來表示，變數 one，two，three，分別記錄每個位元出現的次數

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
    int singleNumber(vector<int>& nums) {
        int one = 0, two = 0, three = 0;

        for (auto i: nums) {
            two |= i & one;
            one ^= i;
            three = one & two;
            one &= ~three;
            two &= ~three;
        }

        return one;
    }
};
```

### Solution 2

第二個方法是通用的解法，可以解決所有 N 個數字相同只有 1 個數字不同的問題

用一個大小為 32 的 bitCnt 陣列來存每個位元出現的次數，最後再對每個 bit 以 N 做餘數運算，只有出現一次的數字餘數會不等於零，再把每個 bit 都加起來就是答案

``` c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int bitCnt[32] = {0};

        for (auto num: nums) {
            int n = num;
            for (int i = 0; i < 32; i++) {
                bitCnt[i] += n & 1;
                n >>= 1;

                if (n == 0)
                    break;
            }
        }

        int result = 0;
        for (int i = 0; i < 32; i++) {
            if (bitCnt[i] % 3 == 0)
                continue;

            result += (1 << i);
        }

        return result;
    }
};
```
