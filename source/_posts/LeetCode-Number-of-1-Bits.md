title: "[LeetCode] Number of 1 Bits"
date: 2015-03-14 23:06:16
categories: LeetCode
tags:
- LeetCode
- C/C++
- Bit Manipulation
---
計算當一個數字用二進位來表示時，總共有多少個位元為 1

<!-- more -->

###Solution 1

第一個方法很直覺，每個位元都判斷一次，32 位元比對 32 次之後就能知道結果

``` c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
       int count = 0;
       uint32_t mask = 1;

       for (int i = 0; i < 32; i++, mask <<= 1) {
           if (n & mask)
               count++;
       }

       return count;
    }
};
```

###Solution 2

第二個方法利用 C++ STL 提供的 bit-array 結構，直接算出答案

``` c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
       bitset<32> b(n);
       return b.count();
    }
};
```

###Solution 3

第三個方法是從 [Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight) 看來的，每次都把 n 與 n - 1 做 AND 運算，每做一次運算，n 都會少掉最右邊的 1，所以用這個方法的話，有多少個位元為 1，就會做幾次 AND 運算

``` c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
       int count = 0;
       for (count; n; count++)
           n &= (n - 1);

       return count;
    }
};
```
