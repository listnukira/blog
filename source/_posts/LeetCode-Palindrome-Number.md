title: "[LeetCode] Palindrome Number"
date: 2014-11-22 12:07:13
categories: LeetCode
tags:
- LeetCode
- C/C++
- Math
---
判斷數字是不是迴文

<!-- more -->

### Solution 1

第一個方法先找出數字是幾位數的，之後從左右兩邊來判斷數字是否相同

``` c++
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0)
            return false;

        int leftDigit = 1000000000;
        int rightDigit = 1;

        while (leftDigit != 1 && (x / leftDigit) == 0)
            leftDigit /= 10;

        while (leftDigit > rightDigit) {
            if ((x / leftDigit) % 10 != (x / rightDigit) % 10)
                return false;

            leftDigit /= 10;
            rightDigit *= 10;
        }

        return true;
    }
};
```

### Solution 2

第二個方法用 [Reverse Integer](/-LeetCode-Reverse-Integer/) 的方式將題目給的數字反轉，反轉完如果相等代表就是迴文

``` c++
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0)
            return false;

        int revX = 0;
        int tempX = x;

        while (tempX != 0) {
            revX = revX * 10 + (tempX % 10);
            tempX /= 10;
        }

        return (revX == x);
    }
};
```
