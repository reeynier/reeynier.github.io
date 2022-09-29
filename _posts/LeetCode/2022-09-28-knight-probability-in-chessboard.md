---
layout: post
title: "Knight Probability In Chessboard Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 688. On an n x n chessboard, a knight starts at the cell (row, column) and attempts to make exactly k moves. The rows and columns are 0-indexed, so the top-left cell is (0, 0), and the bottom-right cell is (n - 1, n - 1).

---

<br />

## Description

LeetCode Problem 688.

On an n x n chessboard, a knight starts at the cell (row, column) and attempts to make exactly k moves. The rows and columns are 0-indexed, so the top-left cell is (0, 0), and the bottom-right cell is (n - 1, n - 1).

A chess knight has eight possible moves it can make, as illustrated below. Each move is two cells in a cardinal direction, then one cell in an orthogonal direction.

Each time the knight is to move, it chooses one of eight possible moves uniformly at random (even if the piece would go off the chessboard) and moves there.

The knight continues moving until it has made exactly k moves or has moved off the chessboard.

Return the probability that the knight remains on the board after it has stopped moving.

Example 1:
```
Input: n = 3, k = 2, row = 0, column = 0
Output: 0.06250
Explanation: There are two moves (to (1,2), (2,1)) that will keep the knight on the board.
From each of those positions, there are also two moves that will keep the knight on the board.
The total probability the knight stays on the board is 0.0625.
```

Example 2:
```
Input: n = 1, k = 0, row = 0, column = 0
Output: 1.00000
```

Constraints:
* 1 <= n <= 25
* 0 <= k <= 100
* 0 <= row, column <= n

<br />

## Sample C++ Code


```c
class Solution {
public:
    double helperFunction(int N, int K, int r, int c, vector<vector<vector<double>>> & dp) {
        if (r < 0 || c < 0 || r >= N || c >= N) 
            return 0;
        if (K == 0) 
            return 1;
        if (dp[r][c][K] != -1) 
            return dp[r][c][K];
        double sum = helperFunction(N, K - 1, r - 2, c - 1, dp) +
                     helperFunction(N, K - 1, r - 1, c - 2, dp) +
                     helperFunction(N, K - 1, r + 1, c - 2, dp) +
                     helperFunction(N, K - 1, r + 2, c - 1, dp) +
                     helperFunction(N, K - 1, r - 2, c + 1, dp) +
                     helperFunction(N, K - 1, r - 1, c + 2, dp) +
                     helperFunction(N, K - 1, r + 1, c + 2, dp) +
                     helperFunction(N, K - 1, r + 2, c + 1, dp);
        sum = sum / 8;
        dp[r][c][K] = sum;
        return dp[r][c][K];
    }
    double knightProbability(int N, int K, int r, int c) {
        vector<vector<vector<double>>> dp(N + 1, vector<vector<double>> (N + 1, vector<double>(K + 1, -1)));
        return helperFunction(N, K, r, c, dp);
    }
};
```


