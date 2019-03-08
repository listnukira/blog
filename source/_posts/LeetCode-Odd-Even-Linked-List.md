title: '[LeetCode] Odd Even Linked List'
date: 2016-03-08 00:37:22
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
toc: false
---
給一個單向串列，將奇數節點依照順序放在串列的前半段，偶數節點放在串列的後半段

<!-- more -->

### Solution

將串列分成奇數串列跟偶數串列，最後把偶數串列接在奇數串列後面

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
    ListNode* oddEvenList(ListNode* head) {
        ListNode *evenHead, *oddHead;
        ListNode *even, *odd;

        if (head == NULL)
            return head;

        oddHead = odd = head;
        evenHead = even = head->next;

        while (odd->next && even->next) {
            odd->next = even->next;
            odd = odd->next;

            even->next = odd->next;
            even = even->next;
        }

        odd->next = evenHead;

        return oddHead;
    }
};
```
