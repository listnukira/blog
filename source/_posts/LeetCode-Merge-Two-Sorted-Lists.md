title: "[LeetCode] Merge Two Sorted Lists"
date: 2014-11-26 17:43:59
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
---
把兩個排序好的串列合併成一個排序好的串列

<!-- more -->

### Solution 1

第一個方法用 iteration 的方式，判斷兩個串列的大小，小的加到 fakeHead 後面，當 while 迴圈結束之後，l1 或 l2 會有一個是 NULL，把不是 NULL 的串列接到 fakeHead 的最後

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
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2) {
        ListNode *fakeHead = new ListNode(0);
        ListNode *head = fakeHead;

        while (l1 != NULL && l2 != NULL) {
            if (l2->val > l1->val) {
                fakeHead->next = l1;
                l1 = l1->next;
            } else {
                fakeHead->next = l2;
                l2 = l2->next;
            }
            fakeHead = fakeHead->next;
        }

        fakeHead->next = (l1 == NULL) ? l2 : l1;

        return head->next;
    }
};
```

### Solution 2

第二個方法用 recursive 的方式，程式碼比較簡潔

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
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2) {
        if (l1 == NULL)
            return l2;

        if (l2 == NULL)
            return l1;

        if (l1->val > l2->val) {
            l2->next = mergeTwoLists(l1, l2->next);
            return l2;
        } else {
            l1->next = mergeTwoLists(l2, l1->next);
            return l1;
        }
    }
};
```
