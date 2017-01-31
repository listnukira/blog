title: "[LeetCode] Remove Duplicates from Sorted List"
date: 2014-09-11 21:13:13
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
toc: false
---
給一個已經排序好的整數串列，把重複的整數刪到只剩一個，並回傳新的串列

<!-- more -->

### Solution

用一個 cur 指標，從頭開始走遍串列，如果下一個節點的值跟自己一樣就跳過

``` c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* deleteDuplicates(struct ListNode* head) {
    struct ListNode *cur = head;

    while (cur && cur->next) {
        if (cur->val == cur->next->val)
            cur->next = cur->next->next;
        else
            cur = cur->next;
    }

    return head;
}
```
