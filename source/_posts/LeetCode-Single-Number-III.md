title: '[LeetCode] Single Number III'
date: 2016-01-11 21:46:54
categories: LeetCode
tags:
- LeetCode
- C/C++
- Bit Manipulation
---
給一個整數陣列，每個數字都會出現兩次，有兩個數字會各出現一次，要找出這兩個數字

<!-- more -->

[Single Number](/LeetCode-Single-Number-II) 的進階版

假設這兩個數字分別為 J 和 K，由於會各出現一次，所以把全部數字做 XOR 運算只會得到這兩個數字 XOR 的結果，也就是 `J XOR K`，而且也無法從這個結果找出 J 和 K，但是可以確定 `J XOR K` 一定不等於零，而 `J XOR K` 的結果 bit 等於 1 代表 J 跟 K 在這個 bit 上，一定一個是 1，一個是 0，假設第三個 bit 是 1，可以根據這個 bit 把所有的數字分成兩群，有一群第三個 bit 全是 1，另一群全是 0，如此一來能把 J 和 K 分開，而且同樣的數字也會被分在同一堆，這兩群數字再分別做 XOR 運算，就可以得到 J 和 K

Note: 即使 J XOR K 的結果有很多個 bit 為 1，也只需要使用到一個位元，為了方便就統一找最右邊第一個為 1 的 bit

Note 2: 找最右邊第一個為 1 的 bit 的方法除了 `A & -A` 之外，還有 `(A ^ (A - 1) & A)`

### Solution

```c++
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        int xorResult = 0;

        for (auto num: nums)
            xorResult ^= num;

        int A = 0, B = 0;
        int lastNonZeroBit = xorResult & (-xorResult);
        for (auto num: nums) {
            if ((num & lastNonZeroBit) == 0)
                A ^= num;
            else
                B ^= num;
        }

        return vector<int>{A, B};
    }
};
```

### Reference

[Two numbers appearing once in array](http://www.codinghelmet.com/?path=exercises/two-numbers-appearing-once-in-array)
