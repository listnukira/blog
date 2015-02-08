title: "[LeetCode] Convert Sorted List to Binary Search Tree"
date: 2015-01-27 22:45:41
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
- Depth-first Search
---
把排序過的串列轉成平衡的二元搜尋樹

<!-- more -->

與 [Convert Sorted Array to Binary Search Tree](/-LeetCode-Convert-Sorted-Array-to-Binary-Search-Tree/) 類似的題目，不同的地方在於與排序過的陣列相比，排序過的串列存取中間的元素不再是 O(1) 的時間複雜度

###Solution 1

第一個方法與 [Convert Sorted Array to Binary Search Tree](/-LeetCode-Convert-Sorted-Array-to-Binary-Search-Tree/) 類似，找出串列的中間節點當作根節點，串列的左邊與右邊也以同樣的方式新增節點

這個方法的時間複雜度為 O(NlogN)

``` c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode *sortedListToBST(ListNode *head) {
        return sortedListToBST(head, NULL);
    }

    TreeNode *sortedListToBST(ListNode *head, ListNode *tail) {
        if (head == tail)
            return NULL;

        if (head->next == tail)
            return new TreeNode(head->val);

        ListNode *mid, *temp;
        mid = temp = head;
        while (temp != tail && temp->next != tail) {
            mid = mid->next;
            temp = temp->next->next;
        }

        TreeNode *node = new TreeNode(mid->val);
        node->left = sortedListToBST(head, mid);
        node->right = sortedListToBST(mid->next, tail);

        return node;
    }
};
```

###Solution 2

第二個方法是參考底下 Reference 網站寫出來的

第一個方法用 top-down 的方式建立平衡二元樹，第二個方法使用 bottom-up 來建立

需要特別注意的地方是在傳遞 Node 參數時，要傳指標的位址，如此一來在遞迴的過程中，head 才會慢慢往後移動

這個方法的時間複雜度為 O(N)

``` c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode *sortedListToBST(ListNode *head) {
        int n = 0;

        ListNode *temp = head;
        while (temp != NULL) {
            n++;
            temp = temp->next;
        }

        return sortedListToBST(&head, 0, n - 1);
    }

    TreeNode *sortedListToBST(ListNode **list, int start, int end) {
        if (start > end)
            return NULL;

        int mid = (start + end) / 2;

        TreeNode *leftNode = sortedListToBST(list, start, mid - 1);
        TreeNode *parent = new TreeNode((*list)->val);

        parent->left = leftNode;
        *list = (*list)->next;
        parent->right = sortedListToBST(list, mid + 1, end);

        return parent;
    }
};
```

---
Reference:
[LeetCode - Convert Sorted List to BST](http://leetcode.com/2010/11/convert-sorted-list-to-balanced-binary.html)
[GeeksforGeeks - Sorted Linked List to Balanced BST](http://www.geeksforgeeks.org/sorted-linked-list-to-balanced-bst/)
