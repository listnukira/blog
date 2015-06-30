title: "[LeetCode] Two Sum"
date: 2015-05-01 01:06:37
categories: LeetCode
tags:
- LeetCode
- C/C++
- Array
- Hash Table
---
給一個整數陣列，找出兩個數字，加起來等於題目給的值，並且回傳索引值

<!-- more -->

用暴力法來找會超時，所以用其他方法來解

###Solution 1

第一個方法建立 hash table，由每個數字對應到索引，從陣列開頭開始，每當遇到一個數字，就檢查有沒有在 hash table 裡，如果有就代表找到了，沒有的話就把 `<target - number, index>` 放入 hash table，直到找到為止

```c++
class Solution {
public:
    vector<int> twoSum(vector<int> &numbers, int target) {
        unordered_map<int, int> hashMap;
        vector<int> answers(2);

        for (int i = 0; i < numbers.size(); i++) {
            unordered_map<int, int>::const_iterator it = hashMap.find(numbers[i]);
            if (it != hashMap.end()) {
                answers[0] = it->second;
                answers[1] = i + 1;
                break;
            }

            hashMap.insert({target - numbers[i], i + 1});
        }

        return answers;
    }
};
```

###Solution 2

第二個方法複製一個一樣的陣列然後排序，接著從左右兩邊開始逼近題目給的值，找到後再利用原本的陣列算出索引值

```c++
class Solution {
public:
    vector<int> twoSum(vector<int> &numbers, int target) {
        vector<int> numCopy = numbers;

        sort(numCopy.begin(), numCopy.end());

        int left = 0, right = numCopy.size() - 1;
        while (left < right) {
            int sum = numCopy[left] + numCopy[right];

            if (sum == target) {
                return findIndex(numbers, numCopy[left], numCopy[right]);
            } else if (sum > target) {
                right--;
            } else {
                left++;
            }
        }
    }
private:
    vector<int> findIndex(vector<int> &numbers, int left, int right) {
        vector<int> index;

        for (int i = 0; i < numbers.size(); i++) {
            if (numbers[i] == left || numbers[i] == right)
                index.push_back(i + 1);

            if (index.size() == 2)
                break;
        }

        if (index[0] > index[1])
            swap(index[0], index[1]);

        return index;
    }
};
```
