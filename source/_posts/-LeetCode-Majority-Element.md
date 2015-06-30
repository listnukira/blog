title: "[LeetCode] Majority Element"
date: 2015-02-08 23:40:01
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Bit Manipulation
- Divide and Conquer
---

找出陣列出現超過一半以上的數字 (majority element)，假設陣列不為空，而且 majority element 一定存在

<!-- more -->

###Solution

這題的解法有很多種，這邊用 [Moore voting algorithm](http://www.geeksforgeeks.org/majority-element/) 來解

``` c++
class Solution {
public:
    int majorityElement(vector<int> &num) {
        int index = 0, count = 0;

        for (int i = 0; i < num.size(); i++) {
            count = (num[index] == num[i]) ? count + 1 : count - 1;

            if (count == 0) {
                index = i;
                count = 1;
            }
        }

        return num[index];
    }
};
```
