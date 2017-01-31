title: '[LeetCode] Sum of Two Integers'
categories: LeetCode
tags:
- LeetCode
- C/C++
- Bit Manipulation
date: 2016-09-12 16:52:30
---
計算兩個數字的合，不能用到加跟減

<!-- more -->

不能用到加跟減代表要用位元操作來解，有點像加法器，要考慮到進位的問題

### Solution 1

首先用 `a & b` 算出 a，b 相加需要進位的是哪幾個位元，存在 carry 裡，接著用 `a ^ b` 算出不考慮進位時的相加結果，並指定給 a，再把 carry 往左位移一位元指定給 b，這樣下一次的 a，b 相加就會沒加到的進位值加回去，一直重複直到沒有進位需要相加為止

``` c++
class Solution {
public:
    int getSum(int a, int b) {
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        while (b != 0) {
            int carry = a & b;
            a = a ^ b;
            b = carry << 1;
        }

        return a;
    }
};
```

### Solution 2

跟第一個方法一樣的想法，只是改成遞迴

``` c++
class Solution {
public:
    int getSum(int a, int b) {
        if (b == 0)
            return a;

        int carry = a & b;
        a = a ^ b;

        return getSum(a, carry << 1);
    }
};
```
