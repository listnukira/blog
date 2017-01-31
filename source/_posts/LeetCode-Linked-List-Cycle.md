title: "[LeetCode] Linked List Cycle"
date: 2014-09-01 17:58:39
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
- Two Pointers
toc: false
---
判斷 linked list 有沒有迴圈，而且不要用到額外的空間

<!-- more -->

### Solution

用兩個指標 fast 和 slow，fast 每次往後移動兩步，slow 每次移動一步，如果串列存在迴圈，則這兩個指標一定會有重疊的時候，只要判斷到重疊就代表有迴圈存在

時間複雜度為 O(N)，空間複雜度為 O(1)

P.S. 另一個方法可以用 Hash table 實作，table 裡存放的是節點的位址，有重複代表有迴圈，空間複雜度為 O(N)

``` c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
bool hasCycle(struct ListNode *head) {
    struct ListNode *fast, *slow;

    fast = slow = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;

        if (fast == slow)
            return true;
    }

    return false;
}
```
