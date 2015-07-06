title: '[LeetCode] Insertion Sort List'
date: 2015-07-06 01:13:42
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
- Sort
---
用插入排序法排序串列

<!-- more -->

###Solution

`dummyHead` 指向已經排序好的串列
`nextNode` 指向還沒處理的節點串列頭
`insertNode` 指向下一個要插入排序的節點

第 16 行將 `insertNode` 指定為 `nextNode` 的第一個節點
第 17 行將 `nextNode` 指向下一個節點
19-24 行是插入排序的演算法

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
    ListNode* insertionSortList(ListNode* head) {
        ListNode dummyHead = ListNode(INT_MIN);
        ListNode *nextNode = head;

        while (nextNode) {
            ListNode *insertNode = nextNode;
            nextNode = nextNode->next;

            ListNode *cur = &dummyHead;
            while (cur->next != NULL && cur->next->val < insertNode->val)
                cur = cur->next;

            insertNode->next = cur->next;
            cur->next = insertNode;
        }

        return dummyHead.next;
    }
};

```
