---
layout: post
title: "Surrounded Regions Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Depth-First Search, Breadth-First Search, Union Find, Matrix ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 130. Given an m x n matrix board containing 'X' and 'O', capture all regions that are 4-directionallysurrounded by 'X'.

---

<br />

## Description

LeetCode Problem 130.

Given an m x n matrix board containing 'X' and 'O', capture all regions that are 4-directionallysurrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

Example 1:
```
Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
Explanation: Surrounded regions should not be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.
```

Example 2:
```
Input: board = [["X"]]
Output: [["X"]]
```

Constraints:
* m == board.length
* n == board[i].length
* 1 <= m, n <= 200
* board[i][j] is 'X' or 'O'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    void bfs(vector<vector<char>>& board, char c, 
            queue<pair<int, int>>& bfsQ, int row, int col) {
        pair<int, int> curr;
        int i, j;
        while (!bfsQ.empty()) {
            curr = bfsQ.front();
            bfsQ.pop();
            i = curr.first, j = curr.second;
            if ((i > 0) && (board[i-1][j] == 'O')) {
                board[i-1][j] = c;
                bfsQ.push(make_pair(i-1, j));
            }
            if ((i < row-1) && (board[i+1][j] == 'O')) {
                board[i+1][j] = c;
                bfsQ.push(make_pair(i+1, j));
            }
            if ((j > 0) && (board[i][j-1] == 'O')) {
                board[i][j-1] = c;
                bfsQ.push(make_pair(i, j-1));
            }
            if ((j < col-1) && (board[i][j+1] == 'O')) {
                board[i][j+1] = c;
                bfsQ.push(make_pair(i, j+1));
            }
        }
        return;
    }
    
    void solve(vector<vector<char>>& board) {
        if (board.size() == 0)
            return;
        int row = board.size();
        int col = board[0].size();
        
        queue<pair<int, int>> bfsQ;
        
        for (int i = 0; i < row; i ++) {
            if (board[i][0] == 'O') {
                bfsQ.push(make_pair(i, 0));
                board[i][0] = 'Y';
                bfs(board, 'Y', bfsQ, row, col);
            }
            if (board[i][col-1] == 'O') {
                bfsQ.push(make_pair(i, col-1));
                board[i][col-1] = 'Y';
                bfs(board, 'Y', bfsQ, row, col);
            }
        }
        for (int j = 0; j < col; j ++) {
            if (board[0][j] == 'O') {
                bfsQ.push(make_pair(0, j));
                board[0][j] = 'Y';
                bfs(board, 'Y', bfsQ, row, col);
            }
            if (board[row-1][j] == 'O') {
                bfsQ.push(make_pair(row-1, j));
                board[row-1][j] = 'Y';
                bfs(board, 'Y', bfsQ, row, col);
            }
        }
        for (int i = 1; i < row-1; i ++) {
            for (int j = 1; j < col-1; j ++) {
                if (board[i][j] == 'O') {
                    bfsQ.push(make_pair(i, j));
                    board[i][j] = 'X';
                    bfs(board, 'X', bfsQ, row, col);
                }
                
            }
        }
        
        for (int i = 0; i < row; i ++) {
            for (int j = 0; j < col; j ++) {
                if (board[i][j] == 'Y')
                    board[i][j] = 'O';
            }
        }
        
        return;
    }
};
```


