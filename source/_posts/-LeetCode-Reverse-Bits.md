title: "[LeetCode] Reverse Bits"
date: 2015-03-21 23:13:00
categories: LeetCode
tags:
- LeetCode
- C/C++
- Bit Manipulation
---
反轉由題目給的二進位數字

<!-- more -->

###Solution 1

假設最後要傳回的數字是`value`，題目給的數字為`n`，每次都把`n`最右邊的位元與`value << 1`做聯集運算，如此一來`n`的 LSB 在`value`中會慢慢的被推到左邊，全部做完後，`value`就是反轉後的值

``` c++
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        uint32_t value = 0;
        for (int i = 0; i < 32; i++, n >>= 1)
            value = (value << 1) | (n & 1);

        return value;
    }
};
```

###Solution 2

第二個方法是在 Discuss 看到的，類似 merge sort 的作法，先把前面 16 位元與後面 16 位元交換，接下來再分別交換前後半部前面的 8 位元與後面的 8 位元，之後以此類推，全部做完後就完成了

``` c++
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        n = (n >> 16) | (n << 16);
        n = ((n & 0xff00ff00) >> 8) | ((n & 0x00ff00ff) << 8);
        n = ((n & 0xf0f0f0f0) >> 4) | ((n & 0x0f0f0f0f) << 4);
        n = ((n & 0xcccccccc) >> 2) | ((n & 0x33333333) << 2);
        n = ((n & 0xaaaaaaaa) >> 1) | ((n & 0x55555555) << 1);
        return n;
    }
};
```
