title: '[LeetCode] Power of Two'
date: 2015-07-15 17:57:23
categories: LeetCode
tags:
- LeetCode
- C/C++
- Bit Manipulation
- Math
---
給一個整數，判斷是不是 2 的次方數

<!-- more -->

2 的次方數代表 32 個 bit 裡，只有一個位元為 1，負數一定不是

### Solution 1

第一個方法很直覺，就是跟 2 的次方做 XOR 運算，等於零代表就是 2 的次方數

``` c++
class Solution {
public:
    bool isPowerOfTwo(int n) {
        if (n < 0)
            return false;

        for (int i = 0; i < 32; i++) {
            if (((1 << i) ^ n) == 0)
                return true;
        }

        return false;
    }
};
```

### Solution 2

第二個方法用 C++ 的 bitset 樣板，判斷是不是只有一個 1

``` c++
class Solution {
public:
    bool isPowerOfTwo(int n) {
        if (n < 0)
            return false;

        bitset<32> b(n);
        return b.count() == 1;
    }
};
```

### Solution 3

第三個方法把 n 與 n - 1 做 AND 運算，等於零代表就是 2 的次方數

``` c++
class Solution {
public:
    bool isPowerOfTwo(int n) {
        return (n > 0) && ((n & (n - 1)) == 0);
    }
};
```
