title: '[LeetCode] Ugly Number'
date: 2015-08-26 20:58:04
categories: LeetCode
tags:
- LeetCode
- C/C++
- Math
---
只由 2, 3, 5 組成的數字叫 Ugly Number，判斷一個數字是不是 Ugly Number

<!-- more -->

把 `num` 分別除以 `2, 3, 5` (要除的進)，最後是 `1` 代表就是 Ugly Number

### Solution 1

```c++
class Solution {
public:
    bool isUgly(int num) {
        if (num < 1)
            return false;

        while (num % 5 == 0)
            num /= 5;
        while (num % 3 == 0)
            num /= 3;
        while (num % 2 == 0)
            num /= 2;

        return (num == 1) ? true : false;
    }
};
```

### Solution 2

第二個方法只是簡化第一個方法的程式碼

```c++
class Solution {
public:
    bool isUgly(int num) {
        for (int i = 2; i < 6 && num; i++) {
            while (num % i == 0)
                num /= i;
        }

        return (num == 1) ? true : false;
    }
};
```
