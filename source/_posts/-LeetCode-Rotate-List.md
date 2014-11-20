title: "[LeetCode] Rotate List"
date: 2014-09-21 17:24:50
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
- Two Pointers
---
給一個串列，將串列往右平移 k 次，回傳新的串列

<!-- more -->

###Solution

假設串列長度為 len，將串列的頭跟尾接起來，變成一個迴圈，接下來就可以根據 k 和 len，移動到新串列的最後一個節點，最後一個節點的下一個節點就是新的 head


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
    ListNode *rotateRight(ListNode *head, int k) {
        struct ListNode *cur = head;
        int len = 1;

        if (head == NULL)
            return head;

        while (cur->next != NULL) {
            cur = cur->next;
            len++;
        }
        cur->next = head;

        k = len - (k % len);
        for (int i = 0; i < k; i++)
            cur = cur->next;

        head = cur->next;
        cur->next = NULL;

        return head;
    }
};
```
