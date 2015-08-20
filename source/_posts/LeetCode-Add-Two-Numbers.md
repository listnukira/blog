title: "[LeetCode] Add Two Numbers"
date: 2014-10-03 15:19:39
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
- Math
---
串列以相反的順序表示每個位數，將兩個串列相對應的數字相加，大於 10 要進位到右邊

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
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
        ListNode *curL1 = l1, *curL2 = l2;
        int sum = 0;

        ListNode *fakeHead = new ListNode(0);
        ListNode *cur = fakeHead;
        while (curL1 != NULL || curL2 != NULL) {
            sum /= 10;

            if (curL1 != NULL) {
                sum += curL1->val;
                curL1 = curL1->next;
            }

            if (curL2 != NULL) {
                sum += curL2->val;
                curL2 = curL2->next;
            }

            cur->next = new ListNode(sum % 10);
            cur = cur->next;
        }

        if (sum > 9)
            cur->next = new ListNode(1);

        return fakeHead->next;
    }
};
```
