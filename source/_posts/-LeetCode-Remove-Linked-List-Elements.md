title: "[LeetCode] Remove Linked List Elements"
date: 2015-06-30 16:02:40
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
---

刪除串列裡指定的值，值可能會重複

<!-- more -->

### Solution

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
    ListNode* removeElements(ListNode* head, int val) {
        ListNode fakeHead(0);
        fakeHead.next = head;

        ListNode *cur = &fakeHead;
        while (cur != NULL && cur->next != NULL) {
            ListNode *tmp = cur->next;
            while (tmp != NULL && tmp->val == val)
                tmp = tmp->next;
                
            cur->next = tmp;
            cur = tmp;
        }

        return fakeHead.next;
    }
};
```
