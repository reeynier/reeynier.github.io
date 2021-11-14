---
layout: post
title:  "Word Search Problem"
categories: [ Algorithm ]
tags: [ Array, Backtracking, Leetcode ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 79. Given an m x n grid of characters board and a string word, return true if word exists in the grid.
---

<br />

## Description

LeetCode Problem 79. 

Given an m x n grid of characters board and a string word, return true if word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

 

Example 1:
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

Example 2:
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
```

Example 3:
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
```
 

Constraints:

* m == board.length
* n = board[i].length
* 1 <= m, n <= 6
* 1 <= word.length <= 15
* board and word consists of only lowercase and uppercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string wordS;
    bool ans;
    int r, c;
    
    void backtrack(vector<vector<char>>& board, 
                   int x, int y, int idx) {
        if (ans == true)
            return;
        int len = wordS.size();
        if (idx == len)
            ans = true;
        if (idx >= len)
            return;

        int m, n;
        char oldchar;
        vector<vector<int>> dir = { {-1,0}, {1,0}, {0,-1}, {0,1} };
        for (int i = 0; i < 4; i ++) {
            m = x + dir[i][0];
            n = y + dir[i][1];
            if (m < 0 || m >= r || n < 0 || n >= c)
                continue;
            if (board[m][n] == wordS[idx]) {
                oldchar = board[m][n];
                board[m][n] = '0';
                backtrack(board, m, n, idx+1);
                board[m][n] = oldchar;
            }
        }
        
    }
    
    bool exist(vector<vector<char>>& board, string word) {
        r = board.size(), c = board[0].size();
        
        wordS = word;
        ans = false;
        char oldchar;
        for (int i = 0; i < r; i ++) {
            for (int j = 0; j < c; j ++) {
                if (board[i][j] == wordS[0]) {
                    oldchar = board[i][j];
                    board[i][j] = '0';
                    backtrack(board, i, j, 1);
                    board[i][j] = oldchar;

                }
                if (ans)
                    return true;
            }
        }
        
        return ans;
    }
};
```
