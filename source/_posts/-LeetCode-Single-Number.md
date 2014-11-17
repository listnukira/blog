title: "[LeetCode] Single Number"
date: 2014-08-25 17:29:45
categories: LeetCode
tags:
- LeetCode
- C/C++
- Bit Manipulation
---
給一個整數陣列，每個數字都會出現兩次，只有一個數字會出現一次，要在線性時間並且沒用到額外記憶體的情況下找出這個只出現一次的數字

<!-- more -->

用 XOR 運算子是最簡單且最直覺的方式，相同的數字經過 XOR 之後會變成 0，所以最後會剩下單一的那個數字

### Solution

``` c++
class Solution {
public:
    int singleNumber(int A[], int n) {
        int result = 0;
        for (int i = 0; i < n; i++) {
            result ^= A[i];
        }

        return result;
    }
};
```
