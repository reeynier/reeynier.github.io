---
layout: post
title: "Battleships In A Board Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Depth-First Search, Matrix ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 419. Given an m x n matrix board where each cell is a battleship 'X' or empty '.', return the number of the battleships on board.

---

<br />

## Description

LeetCode Problem 419.

Given an m x n matrix board where each cell is a battleship 'X' or empty '.', return the number of the battleships on board.

Battleships can only be placed horizontally or vertically on board. In other words, they can only be made of the shape 1 x k (1 row, k columns) or k x 1 (k rows, 1 column), where k can be of any size. At least one horizontal or vertical cell separates between two battleships (i.e., there are no adjacent battleships).

Example 1: 
```
Input: board = [["X",".",".","X"],[".",".",".","X"],[".",".",".","X"]]
Output: 2
```

Example 2:
```
Input: board = [["."]]
Output: 0
```

Constraints:
* m == board.length
* n == board[i].length
* 1 <= m, n <= 200
* board[i][j] is either '.' or 'X'.

<br />

## Sample C++ Code

We could define upper left X as the head of battle ship. Then we only need to count the number of heads.

```c
class Solution {
public:
    int countBattleships(vector<vector<char>>& board) {
        if (board.empty() || board[0].empty()) { return 0; }
        int m = board.size(), n = board[0].size(), cnt = 0;
        
        for (int r = 0; r < m; r++)
            for (int c = 0; c < n; c++)
                cnt += board[r][c] == 'X' && (r == 0 || board[r - 1][c] != 'X') && (c == 0 || board[r][c - 1] != 'X');
        
        return cnt;
}
};
```


