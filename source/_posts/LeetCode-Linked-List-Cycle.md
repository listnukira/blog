title: "[LeetCode] Linked List Cycle"
date: 2014-09-01 17:58:39
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
- Two Pointers
---
判斷 linked list 有沒有迴圈

<!-- more -->

###Solution

此題最好的解法就是用 Floyd's Cycle-Finding Algorithm，使用兩個指標 fast 和 slow，fast 每次往後移動兩步，slow 每次移動一步，如果串列存在迴圈，則這兩個指標一定會有重疊的時候，只要判斷到重疊就代表有迴圈存在

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
    bool hasCycle(ListNode *head) {
        struct ListNode *fast = head;
        struct ListNode *slow = head;

        while (fast != NULL && fast->next != NULL) {
            fast = fast->next->next;
            slow = slow->next;

            if (fast == slow)
                return true;
        }

        return false;
    }
};
```
