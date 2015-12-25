title: '[LeetCode] Range Sum Query - Immutable'
date: 2015-12-22 23:56:20
categories: LeetCode
tags:
- LeetCode
- C/C++
- Dynamic Programming
toc: false
---
給一個整數陣列，算出任兩點間的數字和

<!-- more -->

另外用一個陣列存累積的和

以 `1 2 3 4 5 6 7 8 9` 為例，累積的和就是 `1 3 6 10 15 21 28 36 45`，要算出 3 ~ 4 的和就是 `15 - 6 = 9`，把重複的和減掉

### Solution

```c++
class NumArray {
public:
    NumArray(vector<int> &nums) {
        sum.resize(nums.size());

        for (int i = 0; i < nums.size(); i++) {
            if (i == 0)
                sum[i] = nums[i];
            else
                sum[i] = sum[i - 1] + nums[i];
        }
    }

    int sumRange(int i, int j) {
        if (i == 0)
            return sum[j];
        else
            return sum[j] - sum[i - 1];
    }

private:
    vector<int> sum;
};
```
