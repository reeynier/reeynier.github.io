---
layout: post
title: "Minesweeper Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Depth-First Search, Breadth-First Search, Matrix ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 529. Let's play the minesweeper game!

---

<br />

## Description

LeetCode Problem 529.

Let's play the minesweeper game !

You are given an m x n char matrix board representing the game board where:
* 'M' represents an unrevealed mine,
* 'E' represents an unrevealed empty square,
* 'B' represents a revealed blank square that has no adjacent mines (i.e., above, below, left, right, and all 4 diagonals),
* digit ('1' to '8') represents how many mines are adjacent to this revealed square, and
* 'X' represents a revealed mine.

You are also given an integer array click where click = [click_r, click_c] represents the next click position among all the unrevealed squares ('M' or 'E').

Return the board after revealing this position according to the following rules:
* If a mine 'M' is revealed, then the game is over. You should change it to 'X'.
* If an empty square 'E' with no adjacent mines is revealed, then change it to a revealed blank 'B' and all of its adjacent unrevealed squares should be revealed recursively.
* If an empty square 'E' with at least one adjacent mine is revealed, then change it to a digit ('1' to '8') representing the number of adjacent mines.
* Return the board when no more squares will be revealed.

Example 1: 
```
Input: board = [["E","E","E","E","E"],["E","E","M","E","E"],["E","E","E","E","E"],["E","E","E","E","E"]], click = [3,0]
Output: [["B","1","E","1","B"],["B","1","M","1","B"],["B","1","1","1","B"],["B","B","B","B","B"]]
```

Example 2: 
```
Input: board = [["B","1","E","1","B"],["B","1","M","1","B"],["B","1","1","1","B"],["B","B","B","B","B"]], click = [1,2]
Output: [["B","1","E","1","B"],["B","1","X","1","B"],["B","1","1","1","B"],["B","B","B","B","B"]]
```

Constraints:
* m == board.length
* n == board[i].length
* 1 <= m, n <= 50
* board[i][j] is either 'M', 'E', 'B', or a digit from '1' to '8'.
* click.length == 2
* 0 <= click_r < m
* 0 <= click_c < n
* board[click_r][click_c] is either 'M' or 'E'.

<br />

## Sample C++ Code using Depth-First Search 


```c
class Solution {
public:
    int dx[8] = {-1, 0, 1, 0, -1, -1, 1, 1};
    int dy[8] = {0, 1, 0, -1, -1, 1, 1, -1};
    
    bool isValid(vector<vector<char>>& board, int i, int j) {
        return (i >= 0 && j >= 0 && i < board.size() && j < board[0].size());
    }
    
    int hasAdjacentMine(vector<vector<char>>& board, int i, int j) {
        int count = 0;
        for (int k=0; k<8; k++) {
            int I = i + dx[k];
            int J = j + dy[k];
            if (isValid(board, I, J) && board[I][J] == 'M')
                count++;
        }
        return count;
    }
    
    void dfs(vector<vector<char>>& board, vector<vector<bool>>& visited, int i, int j) {
        if (min(i, j) < 0 || i >= board.size() || j >= board[0].size() || visited[i][j]) return;
        visited[i][j] = true;
        if (board[i][j] == 'M') {
            board[i][j] = 'X';
            return;
        }
        if (board[i][j] == 'E') {
            int c = hasAdjacentMine(board, i, j);
            if (c == 0) {
                board[i][j] = 'B';
                for (int k=0; k<8; k++) {
                    dfs(board, visited, i+dx[k], j+dy[k]);
                }
            }
            else {
                board[i][j] = c + '0';
                return;
            }
        }
    }
    
    vector<vector<char>> updateBoard(vector<vector<char>>& board, vector<int>& click) {
        vector<vector<bool>> visited(board.size(), vector<bool>(board[0].size(), false));
        dfs(board, visited, click[0], click[1]);
        return board;
    }
};
```


