title: "[LeetCode] Remove Duplicates from Sorted List"
date: 2014-09-11 21:13:13
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
---
給一個已經排序好的整數串列，把重複的整數刪到只剩一個，並回傳新的串列

<!-- more -->

### Solution

用一個 current 指標，從頭開始走遍串列，如果下一個節點的值跟自己一樣就跳過

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
    ListNode *deleteDuplicates(ListNode *head) {
        struct ListNode *current = head;

        if (head == NULL)
            return head;

        while (current->next != NULL) {
            if (current->val == current->next->val)
                current->next = current->next->next;
            else
                current = current->next;
        }

        return head;
    }
};
```
