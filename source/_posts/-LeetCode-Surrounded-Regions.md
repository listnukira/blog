title: "[LeetCode] Surrounded Regions"
date: 2014-09-19 01:02:19
categories: LeetCode
tags:
- LeetCode
- C/C++
- Breadth-first Search
---
給一個二維的棋盤，裡面只包含 X 和 O，要把被 X 包圍的 O 都變成 X，O 如果有連接到邊緣則不變

<!-- more -->

###Solution

用一個同樣大小的陣列 needFlip 記錄是否要改值，預設都為 true
堆疊 coordinate 記錄需要處理的座標

流程如下
1. 把在邊邊的 O 座標都放進堆疊
2. 處理堆疊裡的座標，用 BFS 將相鄰的 O 都放進堆疊，並將 needFlip 値改成 false
3. 依據 needFlip 修改 board

``` c++
class Solution {
public:
    void solve(vector< vector<char> > &board) {
        if (board.size() == 0)
            return;

        int rowLen = board.size();
        int colLen = board[0].size();

        vector< vector<bool> > needFlip(rowLen, vector<bool>(colLen, true));

        for (int i = 0; i < rowLen; i++) {
            for (int j = 0; j < colLen; j++) {
                if (board[i][j] == 'X')
                    continue;

                if (i == 0 || i == rowLen - 1 || j == 0 || j == colLen - 1)
                    coordinate.push(make_pair(i, j));
            }
        }

        while (!coordinate.empty()) {
            int i = coordinate.top().first;
            int j = coordinate.top().second;
            coordinate.pop();

            needFlip[i][j] = false;
            if (i - 1 >= 0 && board[i - 1][j] == 'O' && needFlip[i - 1][j] == true)
                coordinate.push(make_pair(i - 1, j));

            if (i + 1 < rowLen && board[i + 1][j] == 'O' && needFlip[i + 1][j] == true)
                coordinate.push(make_pair(i + 1, j));

            if (j - 1 >= 0 && board[i][j - 1] == 'O' && needFlip[i][j - 1] == true)
                coordinate.push(make_pair(i, j - 1));

            if (j + 1 < colLen && board[i][j + 1] == 'O' && needFlip[i][j + 1] == true)
                coordinate.push(make_pair(i, j + 1));
        }

        for (int i = 1; i < rowLen - 1; i++)
            for (int j = 1; j < colLen - 1; j++)
                if (needFlip[i][j] == true)
                    board[i][j] = 'X';

    }

private:
    stack< pair<int, int> > coordinate;
};
```
