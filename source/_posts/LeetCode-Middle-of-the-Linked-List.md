title: '[LeetCode] Middle of the Linked List'
categories: LeetCode
tags:
  - LeetCode
  - C/C++
  - Linked List
date: 2018-09-05 21:41:45
---
給一個單向串列，傳回串列的中間節點，如果有兩個中間節點，傳回後面那個

<!-- more -->

### Solution 1

先計算出串列長度，再從頭跑一半長度回傳

``` c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* middleNode(struct ListNode* head) {
    struct ListNode *middle;
    int count = 1;

    middle = head;
    while (middle->next != NULL) {
        middle = middle->next;
        count++;
    }

    middle = head;
    for (int i = 0; i < count / 2; i++) {
        middle = middle->next;
    }

    return middle;
}
```

### Solution 2

用快慢指標來找

``` c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* middleNode(struct ListNode* head) {
    struct ListNode *fast, *slow;

    fast = slow = head;
    while (fast != NULL && fast->next != NULL) {
        fast = fast->next->next;
        slow = slow->next;
    }

    return slow;
}
```
