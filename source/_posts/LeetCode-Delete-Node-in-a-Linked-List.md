title: '[LeetCode] Delete Node in a Linked List'
date: 2015-07-16 11:21:42
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
---
刪除串列中的節點，但只給要刪除的節點，不給串列頭

<!-- more -->

### Solution

因為沒給串列頭，所以不會知道前一個節點的位置，唯一的做法就是把下一個節點的值複製到當前節點，再把下一個節點刪掉

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
    void deleteNode(ListNode* node) {
        ListNode *next = node->next;
        *node = *next;
        delete next;
    }
};
```
