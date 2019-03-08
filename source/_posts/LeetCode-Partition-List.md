title: '[LeetCode] Partition List'
categories: LeetCode
tags:
  - LeetCode
  - C/C++
  - Linked List
  - Two Pointers
toc: false
date: 2018-09-18 01:22:46
---
給一單向串列與數字 x，重新排列串列使得比 x 小的節點在比 x 大的節點前面

<!-- more -->

### Solution

將串列分成比 x 小的跟比 x 大的，分別用 smallHead，bigHead 來記錄串列頭的位置，small，big 來紀錄目前處理到的地方，最後將 small 指到 bigHead，big->next 指向 NULL

``` c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* partition(struct ListNode* head, int x) {
    struct ListNode *small, *smallHead;
    struct ListNode *big, *bigHead;

    small = smallHead = big = bigHead = NULL;
    while (head != NULL) {
        if (head->val < x) {
            if (smallHead == NULL) {
                smallHead = head;
                small = smallHead;
            } else {
                small->next = head;
                small = small->next;  
            }
        } else {
            if (bigHead == NULL) {
                bigHead = head;
                big = bigHead;  
            } else {
                big->next = head;
                big = big->next;                
            }
        }

        head = head->next;
    }

    if (small != NULL)
        small->next = bigHead;
    if (big != NULL)
        big->next = NULL;

    return (small != NULL) ? smallHead : bigHead;
}
```
