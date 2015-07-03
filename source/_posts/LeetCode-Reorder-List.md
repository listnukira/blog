title: "[LeetCode] Reorder List"
date: 2014-09-21 16:01:15
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
---
改變串列的順序，L0→L1→…→Ln-1→Ln 轉成 L0→Ln→L1→Ln-1→L2→Ln-2→…

<!-- more -->

###Solution

先用兩個指標 fast，slow，以 2:1 的速度往後走，當 fast 等於 NULL 時，slow 會在串列的中間，接著用一個堆疊 s 存指向節點的指標，把串列中間以後的指標都放進堆疊，再從頭插入串列

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
    void reorderList(ListNode *head) {
        stack<struct ListNode *> s;
        struct ListNode *fast, *slow;

        if (head == NULL)
            return;

        fast = slow = head;
        while (fast != NULL && fast->next != NULL) {
            fast = fast->next->next;
            slow = slow->next;
        }

        while (slow != NULL) {
            s.push(slow);
            slow = slow->next;
        }

        fast = head;
        while (!s.empty()) {
            s.top()->next = fast->next;
            fast->next = s.top();
            s.pop();
            fast = fast->next->next;
        }
        fast->next = NULL;
    }
};
```
