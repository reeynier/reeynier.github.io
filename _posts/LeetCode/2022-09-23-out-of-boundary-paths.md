---
layout: post
title: "Out Of Boundary Paths Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 576. There is an m x n grid with a ball. The ball is initially at the position [startRow, startColumn]. You are allowed to move the ball to one of the four adjacent cells in the grid (possibly out of the grid crossing the grid boundary). You can apply at most maxMove moves to the ball.

---

<br />

## Description

LeetCode Problem 576.

There is an m x n grid with a ball. The ball is initially at the position [startRow, startColumn]. You are allowed to move the ball to one of the four adjacent cells in the grid (possibly out of the grid crossing the grid boundary). You can apply at most maxMove moves to the ball.

Given the five integers m, n, maxMove, startRow, startColumn, return the number of paths to move the ball out of the grid boundary. Since the answer can be very large, return it modulo 10^9 + 7.

Example 1: 
```
Input: m = 2, n = 2, maxMove = 2, startRow = 0, startColumn = 0
Output: 6
```

Example 2: 
```
Input: m = 1, n = 3, maxMove = 3, startRow = 0, startColumn = 1
Output: 12
```

Constraints:
* 1 <= m, n <= 50
* 0 <= maxMove <= 50
* 0 <= startRow < m
* 0 <= startColumn < n

<br />

## Sample C++ Code


```c
class Solution {
public:
    int dp[51][51][52];
    int mod = 1e9 + 7;
    
    int countPath(int &m,int &n,int x, int r,int c) {
        if (r == m || c == n || r < 0 || c < 0)
            return 1; //reached outside the boundary 
        if (x == 0)
            return 0; //no more moves left;
        int ans = 0;
        if (dp[r][c][x] != -1)
            return dp[r][c][x];
        
        ans = (ans + countPath(m, n, x - 1, r - 1, c)) % mod; //up
        ans = (ans + countPath(m, n, x - 1, r + 1, c)) % mod; //down
        ans = (ans + countPath(m, n, x - 1, r, c + 1)) % mod; //right
        ans = (ans + countPath(m, n, x - 1, r, c - 1)) % mod; //left     
        return dp[r][c][x] = ans;
    }
    
    int findPaths(int m, int n, int maxMove, int startRow, int startColumn) {
        memset(dp, -1, sizeof(dp));
        return countPath(m, n, maxMove, startRow, startColumn);
    }
};
```


