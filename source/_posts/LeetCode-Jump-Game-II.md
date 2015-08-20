title: "[LeetCode] Jump Game II"
date: 2014-11-26 15:12:36
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Greedy
---
[Jump Game](/-LeetCode-Jump-Game/) 的延伸，要算出最少的 jump 數

<!-- more -->

### Solution

以 `2 3 1 1 4` 為例子，會用到三個變數
<pre>
last 代表目前的 jump 最多可以跳到哪個 index
setp 記錄最多可以跳到哪個 index
jumpNum 記錄目前的 jump 數
</pre>

`index = 0` ，更新 step，`step = 2`
`index = 1` ，`index > last`，代表可用的步數用完了，更新 last，`last = step = 2`，此時 last代表下次最多可以跳到哪個 index，之後更新 step，`step = 4`，`jumpNum++`
`index = 2` ，更新 step，此時 setp = 4
`index = 3` ，`index > last`，更新 last，`last = step = 4`，`jumpNum++`
`index = 4` ，更新 step，此時 step = 4

``` c++
class Solution {
public:
    int jump(int A[], int n) {
        int last = 0, step = 0, jumpNum = 0;

        for (int i = 0; i < n; i++) {
            if (i > last) {
                last = step;
                jumpNum++;
            }

            step = max(step, A[i] + i);
        }

        return jumpNum;
    }
};
```
