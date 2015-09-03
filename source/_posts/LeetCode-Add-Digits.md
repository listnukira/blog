title: '[LeetCode] Add Digits'
date: 2015-09-03 13:36:16
categories: LeetCode
tags:
- LeetCode
- C/C++
- Math
toc: false
---

找出數字的數字根

<!-- more -->

一個數字 N 把每個位數相加，直到只剩下一個位數，這個位數就叫做 N 的數字根

### Solution

與數學比較有關係，從 [Wiki](https://en.wikipedia.org/wiki/Digital_root) 的說明可以得到以下結論

For base b (decimal case b = 10)
* dr(n) = 0 if n == 0
* dr(n) = (b - 1) if n != 0 and n % (b - 1) == 0
* dr(n) = n mod (b - 1) if n % (b - 1) != 0

上面的條件可以簡化成

* dr(n) = 1 + (n - 1) % (b - 1)

Note: `b - 1` 是因為數字根只有 `b - 1 ` 種可能，以 10 來說就是 1 ~ 9

觀察輸入與輸出，可以看出數字根是有規律的

<pre>
input : 0 1 2 3 4 5 6 7 8 9 10 11
output: 0 1 2 3 4 5 6 7 8 9  1  2
</pre>

```c++
class Solution {
public:
    int addDigits(int num) {
        return 1 + (num - 1) % 9;
    }
};
```
