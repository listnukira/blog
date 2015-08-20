title: "[LeetCode] Rotate Array"
date: 2015-04-28 10:40:47
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
---

把一個陣列往右平移 k 次

<!-- more -->

### Solution 1

第一個方法最直覺也最簡單，就是直接複製一個一樣的陣列，然後分別放好

``` c++
class Solution {
public:
    void rotate(int nums[], int n, int k) {
        vector<int> numsCopy(nums, nums + n);

        for (int i = 0; i < n; i++)
            nums[(k + i) % n] = numsCopy[i];
    }
};
```

### Solution 2

第二個方法是在 Discuss 裡看到的，先把後面 k 個元素反轉，再把前面的反轉，最後反轉整個陣列

``` c++
class Solution {
public:
    void rotate(int nums[], int n, int k) {
        k %= n;

        // Reverse last k numbers
        reverse(nums + n - k, nums + n);

        // Reverse first n - k numbers
        reverse(nums, nums + n - k);

        // Reverse all numbers
        reverse(nums, nums + n);
    }
};
```

### Solution 3

第 3 個方法需要稍微解釋一下

以`1 2 3 4 5 6 7，n = 7，k = 4`為例

因為要往右平移 4 次，所以把前面 4 個數字跟後面 4 個數字交換，在交換前先將 k mod n，以免 k 超過 n，換的過程如下

<pre>
1 2 3 4 5 6 7 // swap 1 4
4 2 3 1 5 6 7 // swap 2 5
4 5 3 1 2 6 7 // swap 3 6
4 5 6 1 2 3 7 // swap 1 7
4 5 6 7 2 3 1
</pre>

換完之後前面 4 個數字已經在正確的位置了，所以變成要對後面 3 個元素做平移

而這時要處理的陣列變為`2 3 1，n = 7 - 4, k = 4 % 3`，以同樣的方式做交換，因為現在 k = 1 所以把前面 1 個與後面 1 個交換

換的過程如下，

<pre>
2 3 1 // swap 2 1
1 3 2
</pre>

換完後 1 已經在正確的位置了，問題變為`3 2，n = 3 - 1, k = 1 % 2`，以同樣方式交換，直到`k = 0`

```c++
class Solution {
public:
    void rotate(int nums[], int n, int k) {
        for (; k %= n; n -= k, nums += k)
            for(int i = 0; i < k; i++)
                swap(nums[i], nums[n - k + i]);
    }
};
```
