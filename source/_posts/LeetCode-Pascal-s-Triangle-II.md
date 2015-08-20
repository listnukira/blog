title: "[LeetCode] Pascal's Triangle II"
date: 2014-08-28 12:05:20
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
---
Pascal's Triangle 的延伸，只要回傳特定列的陣列

<!-- more -->

### Solution 1

方法一只是稍微修改原本的方法，一層一層算到指定的列，但是會用到多餘的空間

``` c++
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector< vector<int> > triangle(rowIndex + 1);

        triangle[0].push_back(1);
        for (int i = 1; i < rowIndex + 1; i++) {

            triangle[i].push_back(1);
            for (int j = 1; j < i; j++) {
                triangle[i].push_back(triangle[i - 1][j - 1] + triangle[i - 1][j]);
            }
            triangle[i].push_back(1);
        }

        return triangle[rowIndex];
    }
};
```

### Solution 2

第二個方法利用數學組合數直接算出數字，需要小心 overflow 的問題，不會用到多餘的空間

``` c++
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector<int> row(rowIndex + 1, 1);
        long long int up, down;
        up = rowIndex;
        down = 1;

        for (int i = 1; i <= (rowIndex + 1) / 2; i++) {
            row[i] = row[rowIndex - i] = (row[i - 1] * up) / down;

            up--;
            down++;
        }

        return row;
    }
};
```

### Solution 3

第三個方法也是一層一層算，但是不會用到額外的空間，每一次都由陣列的最後往前重算出新的值，以 `1 3 3 1` 求出下一列 `1 4 6 4 1` 為例

``` bash
1 3 3 1
       \|
1 3 3 1 1 // row[4] = row[4] + row[3]
     \|
1 3 3 4 1 // row[3] = row[3] + row[2]
   \|
1 3 6 4 1 // row[2] = row[2] + row[1]
 \|
1 4 6 4 1 // row[1] = row[1] + row[0]
```

程式碼如下

``` c++
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector<int> row(rowIndex + 1, 0);

        row[0] = 1;
        for (int i = 1; i <= rowIndex; i++) {
            for(int j = i; j > 0; j--) {
                row[j] += row[j - 1];
            }
        }

        return row;
    }
};
```
