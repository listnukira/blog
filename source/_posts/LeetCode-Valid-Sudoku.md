title: "[LeetCode] Valid Sudoku"
date: 2014-12-03 17:25:50
categories: LeetCode
tags:
- LeetCode
- C/C++
- Hash Table
---
根據 [Sudoku Puzzles - The Rules](http://sudoku.com.au/TheRules.aspx)，判斷數讀是否合法

<!-- more -->

###Solution

用 C++ 的 `unordered_set` 來做，每行每列加上每個區塊，總共有 27 個 `unordered_set`，接著便可以判斷有沒有重複

``` c++
class Solution {
public:
    bool isValidSudoku(vector<vector<char> > &board) {
        unordered_set<char> set[27];
        pair<unordered_set<char>::iterator, bool> ret;

        for (int i = 0; i < board.size(); i++) {
            for (int j = 0; j < board[0].size(); j++) {
                if (board[i][j] == '.')
                    continue;

                ret = set[i].insert(board[i][j]);
                if (!ret.second)
                    return false;

                ret = set[j + 9].insert(board[i][j]);
                if (!ret.second)
                    return false;

                ret = set[(i / 3) * 3 + (j / 3) + 18].insert(board[i][j]);
                if (!ret.second)
                    return false;
            }
        }

        return true;
    }
};
```
