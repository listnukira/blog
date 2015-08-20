title: '[LeetCode] Reverse Linked List'
date: 2015-07-04 22:57:55
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
---
反轉串列

<!-- more -->

分別用迭代和遞迴來解

### Solution 1

第一個方法用迭代

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
    ListNode* reverseList(ListNode* head) {
        ListNode *newHead = NULL;
        ListNode *cur;

        while (head != NULL) {
            cur = head;
            head = head->next;
            cur->next = newHead;
            newHead = cur;
        }

        return newHead;
    }
};
```

### Solution 2

第二個方法用遞迴，`reverseList(head->next)` 會傳回反轉後的串列頭，而 `head->next` 會指向反轉後的串列尾，`head->next->next = head` 把串列尾改指向 `head`，再將 `head->next` 指向 NULL，這樣就又反轉了一個節點，再將反轉後的串列頭回傳

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
    ListNode* reverseList(ListNode* head) {
        if (head == NULL || head->next == NULL)
            return head;

        ListNode *newHead = reverseList(head->next);

        head->next->next = head;
        head->next = NULL; 

        return newHead;
    }
};
```
