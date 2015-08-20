title: "[LeetCode] Remove Nth Node From End of List"
date: 2014-09-09 21:04:40
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
- Two Pointers
---
移除串列從後面數來的第 N 個節點

<!-- more -->

### Solution

1. 宣告兩個指標 first 和 second，一開始都指向 head
2. second 往後移動 N 個節點，如果移動完之後 second 等於 NULL，代表要刪除的是第一個節點，回傳第二個節點
3. first 和 second 同時往後移動，直到 second->next 等於 NULL 為止
4. 要刪除的節點會是 first->next

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
    ListNode *removeNthFromEnd(ListNode *head, int n) {
        struct ListNode *first, *second;
        first = second = head;

        for (int i = 0; i < n; i++)
            second = second->next;

        if (second == NULL)
            return first->next;

        while (second->next != NULL) {
            first = first->next;
            second = second->next;
        }

        struct ListNode* delNode = first->next;
        first->next = delNode->next;

        return head;
    }
};
```
