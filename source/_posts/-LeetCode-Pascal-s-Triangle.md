title: "[LeetCode] Pascal's Triangle"
date: 2014-08-28 10:53:07
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
---
根據題目給的數字，回傳由巴斯卡三角形組成的陣列

<!-- more -->

###Solution

巴斯卡三角形每一列的數字，除了最左邊跟最右邊的 1，其它的數字都是由上一列相鄰的兩個數字相加而來，可以用很直覺的方式寫出來，如果 numRows 超過 35，就會發生 overflow 了

``` c++
class Solution {
public:
    vector<vector<int> > generate(int numRows) {
        vector< vector<int> > triangle(numRows);

        if (numRows <= 0)
            return triangle;

        triangle[0].push_back(1);
        for (int i = 1; i < numRows; i++) {

            triangle[i].push_back(1);
            for (int j = 1; j < i; j++) {
                triangle[i].push_back(triangle[i - 1][j - 1] + triangle[i - 1][j]);
            }
            triangle[i].push_back(1);
        }

        return triangle;
    }
};
```
