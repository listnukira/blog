title: '[LeetCode] Nim Game'
date: 2015-11-21 14:18:38
categories: LeetCode
tags:
- LeetCode
- C/C++
- Brain teaser
toc: false
---
判斷能否贏得 Nim Game

<!-- more -->

### Solution

Nim Game - 假設桌上有一疊石頭，每次可以拿走一到三個，兩個人輪流拿，拿走最後一個石頭的獲勝

當桌上剩下一個兩個或三個石頭時，可以全部都拿走，所以一定獲勝，但是當只剩四個時，不管怎麼拿都會讓對方獲勝，接著再往上推，當五六七個時，都有辦法拿到桌上只剩四個讓對方輸，當剩八個時，不管怎麼拿都會剩下五六七個讓對方贏，以此類推，只要是四的倍數就會輸

``` c++
class Solution {
public:
    bool canWinNim(int n) {
        return !(n % 4 == 0);
    }
};
```
