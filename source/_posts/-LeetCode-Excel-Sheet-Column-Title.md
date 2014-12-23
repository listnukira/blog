title: "[LeetCode] Excel Sheet Column Title"
date: 2014-12-21 21:53:44
categories: LeetCode
tags:
- LeetCode
- C/C++
- Math
---
給一個正整數，回傳與 Excel Sheet 列對應的 Title

<!-- more -->

###Solution

根據以下規則做換算

<pre>
1 -> A
2 -> B
...
26-> Z
27-> AA
28-> AB
...
52-> AZ
53-> BA
</pre>

``` c++
class Solution {
public:
    string convertToTitle(int n) {
        string title = "";

        while (n) {
            char c = (n - 1) % 26 + 'A';
            title = c + title;
            n = (n - 1) / 26;
        }

        return title;
    }
};
```
