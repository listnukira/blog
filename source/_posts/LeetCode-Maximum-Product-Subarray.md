title: "[LeetCode] Maximum Product Subarray"
date: 2014-09-26 17:45:52
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Dynamic Programming
---
計算陣列裡連續數字相乘的最大值

<!-- more -->

### Solution 1

暴力法，把全部的可能都算出來找最大值，但是會超時

``` c++
class Solution {
public:
    int maxProduct(int A[], int n) {
        int max = 0, product = 1;

        for (int i = 0; i < n; i++) {
            if (A[i] > max)
                max = A[i];

            product = 1;
            for (int j = i; j < n; j++) {
                product *= A[j];
                if (product > max)
                    max = product;
            }
        }

        return max;
    }
};
```

### Solution 2

從頭開始計算乘積，每次計算都算出最大値和最小值，會需要算出最小值是因為只要再乘上一個負數，就可能成為最大值，這個方法只需要 O(n) 的時間與 O(1) 的空間

``` c++
class Solution {
public:
    int maxProduct(int A[], int n) {
        int maximum, prevMax, prevMin;
        maximum = prevMax = prevMin = A[0];

        for (int i = 1; i < n; i++) {
            int tmpMax = max(max(prevMax * A[i], prevMin * A[i]), A[i]);
            int tmpMin = min(min(prevMax * A[i], prevMin * A[i]), A[i]);
            if (tmpMax > maximum)
                maximum = tmpMax;

            prevMax = tmpMax;
            prevMin = tmpMin;
        }

        return maximum;
    }
};
```
