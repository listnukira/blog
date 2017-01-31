title: "[LeetCode] Remove Nth Node From End of List"
date: 2014-09-09 21:04:40
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
- Two Pointers
toc: false
---
移除串列從後面數來的第 N 個節點

<!-- more -->

### Solution

1. 宣告兩個指標 fast 和 slow，一開始都指向 head
2. fast 先往後移動 N 個節點，如果移動完之後 fast 等於 NULL，代表要刪除的是第一個節點，回傳第二個節點
3. fast 和 slow 同時往後移動，直到 fast->next 等於 NULL 為止
4. 要刪除的節點會是 slow->next

``` c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* removeNthFromEnd(struct ListNode* head, int n) {
    struct ListNode *fast, *slow;

    fast = slow = head;
    for (;n > 0; n--)
        fast = fast->next;

    if (!fast)
        return slow->next;

    while (fast->next) {
        fast = fast->next;
        slow = slow->next;
    }

    slow->next = slow->next->next;

    return head;
}
```
