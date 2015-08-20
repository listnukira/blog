title: '[LeetCode] Palindrome Linked List'
date: 2015-07-13 23:25:11
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
- Two Pointers
---
在 O(N) 時間與 O(1) 空間複雜度下，判斷串列是不是迴文

<!-- more -->

### Solution

把串列前面一半的節點反轉，再跟後面的節點比較，用兩個指標找出中間的節點，找的過程中順便反轉串列，最後指定前面與後面的開始節點位置(右半部的開始位置會因為串列的長度是偶數或奇數而不同)，再依序比較

Note: 這種方法會改變原本的串列，如果規定不能改變原本串列的話，在比較的時候可以順便把串列反轉回去

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
    bool isPalindrome(ListNode* head) {
        ListNode *mid, *tail;
        ListNode *prev = NULL;

        mid = tail = head;
        while (tail && tail->next) {
            mid = mid->next;
            tail = tail->next->next;

            // Reverse
            head->next = prev;
            prev = head;
            head = mid;
        }

        // Compare
        ListNode *left = prev;
        ListNode *right = (tail == NULL) ? head : head->next;
        while (left != NULL) {
            if (left->val != right->val)
                return false;

            left = left->next;
            right = right->next;
        }

        return true;
    }
};
```
