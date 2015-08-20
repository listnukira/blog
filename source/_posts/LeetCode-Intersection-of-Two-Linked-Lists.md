title: "[LeetCode] Intersection of Two Linked Lists"
date: 2014-12-03 13:53:21
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
- Two Pointers
---
找出兩個串列交集的節點，沒有交集則回傳 NULL

<!-- more -->

### Solution

兩個指標 A，B 一開始分別指向兩個串列的起點，接著同時往後走，如果兩個串列長度不一樣，則會有一個串列先走到尾端，假設 A 先走到尾端，則把 A 重新指定為另一個串列 B 的開頭，繼續往後走，接下來會是 B 走到尾端，把 B 重新指定為串列 A 的開頭，繼續往後走，此時如果有交集，A 和 B 會在交集的點遇到，否則會同時走到尾端

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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode *A = headA, *B = headB;

        while (A != NULL && B != NULL && A != B) {
            A = A->next;
            B = B->next;
            
            if (A == B)
                return A;

            A = A ? A : headB;
            B = B ? B : headA;
        }

        return (A == B) ? A : NULL;
    }
};
```
