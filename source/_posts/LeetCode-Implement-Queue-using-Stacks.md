title: '[LeetCode] Implement Queue using Stacks'
date: 2015-07-09 00:43:59
categories: LeetCode
tags:
- LeetCode
- C/C++
- Stack
- Data Structure
---
用 stack 實作 queue

<!-- more -->

相似題: [Implement Stack using Queues](/LeetCode-Implement-Stack-using-Queues)

### Solution

用兩個 stack 來處理，每當 push 的時候，把 nums 裡的通通倒到 helper 裡，新增新的元素到 nums 裡，再把 helper 倒回 nums

``` c++
class Queue {
public:
    // Push element x to the back of queue.
    void push(int x) {
        while (!nums.empty()) {
            helper.push(nums.top());
            nums.pop();
        }

        nums.push(x);

        while (!helper.empty()) {
            nums.push(helper.top());
            helper.pop();
        }
    }

    // Removes the element from in front of queue.
    void pop(void) {
        nums.pop();
    }

    // Get the front element.
    int peek(void) {
        return nums.top();
    }

    // Return whether the queue is empty.
    bool empty(void) {
        return nums.empty();
    }

private:
    stack<int> nums, helper;
};
```
