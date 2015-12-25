title: '[LeetCode] Count Primes'
date: 2015-12-17 00:05:01
categories: LeetCode
tags:
- LeetCode
- C/C++
- Hash Table
- Math
toc: false
---
算出正整數 n 以下有多少質數

<!-- more -->

題目的 Hint 解釋得很詳細，甚至連解答的程式碼都有了...，關鍵就是 [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) 方法，以一個從 2 到 n 的連續數字為例，從 2 開始把所有 2 的倍數標記，接下來找到下一個沒被標記的數字 p ，重複剛剛的動作，把 p 的倍數都標記，再找下一個沒被標記的 p，最後算出沒被標記的數字有幾個就是答案

Note: 標記的動作可以從 p 的平方開始，因為 p 平方以前的數字一定已經被標記過了

### Solution

``` c++
class Solution {
public:
    int countPrimes(int n) {
        bool *isPrime = new bool[n];

        for (int i = 2; i < n; i++)
            isPrime[i] = true;

        for (int i = 2; i * i < n; i++) {
            if (!isPrime[i])
                continue;

            for (int j = i * i; j < n; j += i)
                isPrime[j] = false;
        }

        int count = 0;
        for (int i = 2; i < n; i++) {
            if(isPrime[i])
                count++;
        }

        delete[] isPrime;

        return count;
    }
};
```
