title: "[LeetCode] Reverse Linked List II"
date: 2014-09-23 19:40:12
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
---
反轉串列 m 到 n 的部分

<!-- more -->

### Solution

用四個指標記錄不同的節點，分別是反轉後的頭 reverseHead 跟尾 reverseTail，尾的下一個 connTail，頭的上一個 connHead

``` c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *reverseBetween(ListNode *head, int m, int n) {
        struct ListNode *reverseHead = NULL, *reverseTail = NULL;
        struct ListNode *connHead = NULL, *connTail = NULL;
        struct ListNode *cur = NULL;

        cur = head;
        for (int i = 1; i <= n; i++) {
            if (i == m)
                reverseTail = cur;

            if (i >= m && i <= n) {
                connTail = cur->next;
                cur->next = reverseHead;
                reverseHead = cur;
                cur = connTail;
            } else {
                connHead = cur;
                cur = cur->next;
            }
        }

        if (connHead != NULL)
            connHead->next = reverseHead;

        reverseTail->next = connTail;

        return (m == 1) ? reverseHead : head;
    }
};
```
