title: "[LeetCode] Sort List"
date: 2015-05-12 00:43:54
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
- Sort
---

在 O(NlogN) 的時間裡用固定的空間排序串列

<!-- more -->

###Solution

O(NlogN) 的排序方法也沒有幾個，考慮到 link list 的特性，可以用的方法大概只剩 merge sort 了

我的作法是由下往上做，依序合併 1 個數字，2 個數字，4 個數字...以此類推，步驟如下

1. 算出串列的長度

2. 找出要合併的兩個串列頭，將兩個串列用 split 函式處理成相同的長度 (將兩個串列最後節點指向 NULL)

3. merge 函式用來合併這兩個串列，並且回傳合併後的串列頭，同時傳一個 tail 參數進去，紀錄合併後的串列尾

4. 重複前兩個步驟，並且利用拿到的串列頭和尾的資訊做前處理

```c++
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
    ListNode *sortList(ListNode *head) {
        ListNode fakeNode(0);
        ListNode *prevTail = NULL, *tail = NULL;
        ListNode *cur = head;

        int n = 0;
        while (cur != NULL) {
            n++;
            cur = cur->next;
        }

        cur = head;
        ListNode *list1, *list2;
        for (int step = 1; step <= n; step *= 2) {
            prevTail = &fakeNode;

            while (cur != NULL) {
                list1 = list2 = cur;

                for (int i = 0; i < step && list2 != NULL; i++)
                    list2 = list2->next;

                for (int i = 0; i < (step * 2) && cur != NULL; i++)
                    cur = cur->next;

                split(step, list1);
                split(step, list2);

                prevTail->next = merge(list1, list2, tail);
                prevTail = tail;
            }

            cur = fakeNode.next;
        }

        return fakeNode.next;
    }
private:
    ListNode *merge(ListNode *list1, ListNode *list2, ListNode* &tail) {
        ListNode fakeNode(0);
        ListNode *cur = &fakeNode;

        while (list1 != NULL && list2 != NULL) {
            if (list1->val < list2->val) {
                cur->next = list1;
                list1 = list1->next;
            } else {
                cur->next = list2;
                list2 = list2->next;
            }

            cur = cur->next;
        }

        if (list1 == NULL)
            cur->next = list2;
        else
            cur->next = list1;

        while (cur->next != NULL)
            cur = cur->next;

        tail = cur;
        return fakeNode.next;
    }

    void split(int n, ListNode *list) {
        ListNode *tmp = list;
        for (int i = 0; i < (n - 1) && tmp != NULL; i++)
            tmp = tmp->next;

        if (tmp != NULL)
            tmp->next = NULL;
    }
};
```
