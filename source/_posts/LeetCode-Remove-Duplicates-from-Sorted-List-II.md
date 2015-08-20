title: "[LeetCode] Remove Duplicates from Sorted List II"
date: 2014-09-12 21:23:31
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
---
給一個已經排序好的整數串列，把重複的整數全部刪掉，並回傳新的串列

<!-- more -->

### Solution

新串列的開頭有可能會變動，所以用 fakeHead 來幫忙，`fakeHead.next` 會指向新的串列頭，接著需要過濾掉重複的數字

`for (cur = head->next; cur != NULL && cur->val == head->val; cur = cur->next);`

執行完 for 迴圈後，cur 會指向 head 後的第一個相異的數字，接著判斷 cur 是否剛好是 head 的下一個節點，如果是，代表 head 的值只出現一次，可以把 head 新增到 newList 裡，不是就繼續執行，直到 head 等於 NULL，傳回 `fakeHead.next`

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
        struct ListNode fakeHead(0);
        struct ListNode *cur;
        struct ListNode *newList = &fakeHead;

        while (head != NULL) {
            for (cur = head->next; cur != NULL && cur->val == head->val; cur = cur->next);

            if (head->next == NULL || head->next == cur) {
                newList->next = head;
                newList = newList->next;
                newList->next = NULL;
            }

            head = cur;
        }

        return fakeHead.next;
    }

};
```
