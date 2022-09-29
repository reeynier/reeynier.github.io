---
layout: post
title: "Transform To Chessboard Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Bit Manipulation, Matrix ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 782. You are given an n x n binary grid board. In each move, you can swap any two rows with each other, or any two columns with each other.

---

<br />

## Description

LeetCode Problem 782.

You are given an n x n binary grid board. In each move, you can swap any two rows with each other, or any two columns with each other.

Return the minimum number of moves to transform the board into a chessboard board. If the task is impossible, return -1.

A chessboard board is a board where no 0's and no 1's are 4-directionally adjacent.

Example 1: 
```
Input: board = [[0,1,1,0],[0,1,1,0],[1,0,0,1],[1,0,0,1]]
Output: 2
Explanation: One potential sequence of moves is shown.
The first move swaps the first and second column.
The second move swaps the second and third row.
```

Example 2: 
```
Input: board = [[0,1],[1,0]]
Output: 0
Explanation: Also note that the board with 0 in the top left corner, is also a valid chessboard.
```

Example 3: 
```
Input: board = [[1,0],[1,0]]
Output: -1
Explanation: No matter what sequence of moves you make, you cannot end with a valid chessboard.
```

Constraints:
* n == board.length
* n == board[i].length
* 2 <= n <= 30
* board[i][j] is either0 or 1.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int movesToChessboard(vector<vector<int>>& board) {
        int N = board.size(), row_bal = 0, col_bal = 0, c = 0, d = 0;
        for (int i = 0; i < N; ++i) {
            row_bal += board[0][i] ? 1 : -1;
            col_bal += board[i][0] ? 1 : -1;
            if (i & 1) {
                c += board[0][i];
                d += board[i][0];
            }
        }
        if (row_bal > 1 || row_bal < -1 || col_bal > 1 || col_bal < -1)     
            return -1;
        for (int i = 1; i < N; ++i)
            for (int j = 1; j < N; ++j)
                if (board[i][j] ^ board[i][0] ^ board[0][j] ^ board[0][0])      
                    return -1;
        
        if (!row_bal)      
            return min(N / 2 - c, c) + min(N / 2 - d, d);
        else        
            return (row_bal > 0 ? c : N / 2 - c) + (col_bal > 0 ? d : N / 2 - d);
    }
};
```


