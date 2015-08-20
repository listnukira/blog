title: "[LeetCode] Reverse Integer"
date: 2014-11-22 14:29:43
categories: LeetCode
tags:
- LeetCode
- C/C++
- Math
---
將整數的位數前後反轉，123 變 321，-123 變 -321

<!-- more -->

### Solution

這題比較偏數學計算，關鍵在
`revX = revX * 10 + (x % 10)`
x 的最小位數會因為乘以十慢慢變成最大位數，同時要考慮溢位的情況，因為 32 位元正整數的最大值為 2147483647，所以在乘以十之前必須判斷是否大於 214748364

``` c++
class Solution {
public:
    int reverse(int x) {
        int revX = 0;
        
        while (x != 0) {
            if (abs(revX) > 214748364)
                return 0;

            revX = revX * 10 + (x % 10);
            x /= 10;
        }
        
        return revX;
    }
};
```
