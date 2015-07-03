title: "[LeetCode] Linked List Cycle II"
date: 2014-09-02 18:18:39
categories: LeetCode
tags:
- LeetCode
- C/C++
- Linked List
- Two Pointers
---
延續 [Linked List Cycle](/2014/09/01/-LeetCode-Linked-List-Cycle/)，此題要找出串列裡迴圈開始的起點，沒有迴圈則回傳 NULL

<!-- more -->

###Solution

假設串列開頭到迴圈開頭的距離為 K，迴圈長度為 Y，有兩個指標分別為 fast 跟 slow，現在從串列頭開始移動，fast 每次走兩步，slow 每次走一步，當有迴圈時 fast 跟 slow 會重疊，由迴圈開頭到重疊的地方距離為 M，所以可以得到以下關係

fast 總共走的步數，其中 a 為任意數，因為可能走了好幾圈
`K + aY + M`
slow 總共走的步數，b 為任意數
`K + bY + M`
因為 fast 是 slow 的兩倍
`2(K + bY + M) = K + aY + M`
最後可以得到
`(K + M) = cY`

也就是當重疊的時候 (會在 M 點)，fast 或 slow 只要再走 K 步就會到迴圈的開頭，而 K 剛好是串列開頭到迴圈開頭的距離，所以只要把 fast 或 slow 其中一個指到串列開頭，再用相同速度往前走，此時重疊的地方就是迴圈的起點，大致可以寫成以下 4 個步驟
1. 宣告兩個指標，fast 跟 slow
2. fast 每次走兩步，slow 每次走一步
3. 當 fast 跟 slow 重疊時，將 slow 指到串列的頭，fast 不變
4. fast 跟 slow 一次都前進一步，再次重疊的地方就是迴圈開始的地方

程式碼如下

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
    ListNode *detectCycle(ListNode *head) {
        struct ListNode *fast = head;
        struct ListNode *slow = head;

        while (fast != NULL && fast->next != NULL) {
            fast = fast->next->next;
            slow = slow->next;

            if (fast == slow)
                break;
        }

        if (fast == NULL || fast->next == NULL)
            return NULL;

        slow = head;
        while (slow != fast) {
            fast = fast->next;
            slow = slow->next;
        }

        return fast;
    }
};
```
