title: "[LeetCode] Swap Nodes in Pairs"
date: 2015-05-02 15:05:01
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
---

將串列的節點兩兩交換

<!-- more -->

###Solution

練習 linked list 的題目，圖畫出來就很清楚了

```c++
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
    ListNode *swapPairs(ListNode *head) {
        ListNode fakeHead(0);
        ListNode *cur = head;
        ListNode *prev = &fakeHead;

        fakeHead.next = head;
        while (cur != NULL && cur->next != NULL) {
            prev->next = cur->next;
            cur->next = cur->next->next;
            prev->next->next = cur;
            
            prev = cur;
            cur = cur->next;
        }

        return fakeHead.next;
    }
};
```
