title: '[LeetCode] Implement Stack using Queues'
date: 2015-07-10 00:36:24
categories: LeetCode
tags:
- LeetCode
- C/C++
- Stack
- Data Structure
---
用 queue 實作 stack

<!-- more -->

相似題: [Implement Queue using Stacks](/LeetCode-Implement-Queue-using-Stacks)

###Solution 1

用兩個 queue 來處理，每當 push 的時候，把 nums 裡的通通倒到 helper 裡，新增新的元素到 nums 裡，再把 helper 倒回 nums

``` c++
class Stack {
public:
    // Push element x onto stack.
    void push(int x) {
        while (!nums.empty()) {
            helper.push(nums.front());
            nums.pop();
        }

        nums.push(x);

        while (!helper.empty()) {
            nums.push(helper.front());
            helper.pop();
        }
    }

    // Removes the element on top of the stack.
    void pop() {
        nums.pop();
    }

    // Get the top element.
    int top() {
        return nums.front();
    }

    // Return whether the stack is empty.
    bool empty() {
        return nums.empty();
    }

private:
    queue<int> nums, helper;
};
```

###Solution 2

第二個方法只會用到一個 queue，每次新增的值都會在 queue 的尾端，再把其它的值都吐出來加到 queue 的尾端

``` c++
class Stack {
public:
    // Push element x onto stack.
    void push(int x) {
        nums.push(x);

        int len = nums.size();
        for (int i = 0; i < len - 1; i++) {
            nums.push(nums.front());
            nums.pop();
        }
    }

    // Removes the element on top of the stack.
    void pop() {
        nums.pop();
    }

    // Get the top element.
    int top() {
        return nums.front();
    }

    // Return whether the stack is empty.
    bool empty() {
        return nums.empty();
    }

private:
    queue<int> nums;
};
```
