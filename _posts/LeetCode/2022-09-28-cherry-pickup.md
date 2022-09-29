---
layout: post
title: "Cherry Pickup Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Matrix ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 741. You are given an n x n grid representing a field of cherries, each cell is one of three possible integers.

---

<br />

## Description

LeetCode Problem 741.

You are given an n x n grid representing a field of cherries, each cell is one of three possible integers.
* 0 means the cell is empty, so you can pass through,
* 1 means the cell contains a cherry that you can pick up and pass through, or
* -1 means the cell contains a thorn that blocks your way.
Return the maximum number of cherries you can collect by following the rules below:
* Starting at the position (0, 0) and reaching (n - 1, n - 1) by moving right or down through valid path cells (cells with value 0 or 1).
* After reaching (n - 1, n - 1), returning to (0, 0) by moving left or up through valid path cells.
* When passing through a path cell containing a cherry, you pick it up, and the cell becomes an empty cell 0.
* If there is no valid path between (0, 0) and (n - 1, n - 1), then no cherries can be collected.

Example 1: 
```
Input: grid = [[0,1,-1],[1,0,-1],[1,1,1]]
Output: 5
Explanation: The player started at (0, 0) and went down, down, right right to reach (2, 2).
4 cherries were picked up during this single trip, and the matrix becomes [[0,1,-1],[0,0,-1],[0,0,0]].
Then, the player went left, up, up, left to return home, picking up one more cherry.
The total number of cherries picked up is 5, and this is the maximum possible.
```

Example 2:
```
Input: grid = [[1,1,-1],[1,-1,1],[-1,1,1]]
Output: 0
```

Constraints:
* n == grid.length
* n == grid[i].length
* 1 <= n <= 50
* grid[i][j] is -1, 0, or 1.
* grid[0][0] != -1
* grid[n - 1][n - 1] != -1

<br />

## Sample C++ Code


```c
class Solution {
public:
    int cherryPickup(vector<vector<int>>& grid) {
        int N = grid.size();
        int P_LEN = N + N - 1;
        vector<vector<int> > dp = vector<vector<int>>(N, vector<int>(N, -1));
        dp[0][0] = grid[0][0];
        
        for (int p = 2; p <= P_LEN; p++) {//p is the length of the path
            for (int x1 = N - 1; x1 >= 0; x1--) {
                for (int x2 = x1; x2 >= 0; x2--) {
                    int y1 = p - 1 - x1;
                    int y2 = p - 1 - x2;
                    if (y1 < 0 || y2 < 0 || y1 >= N || y2 >= N)
                        continue;
                    if (grid[y1][x1] < 0 || grid[y2][x2] < 0) {
                        dp[x1][x2] = -1;
                        continue;
                    }   
                    int best = -1, delta = grid[y1][x1];
                    if (x1 != x2)
                        delta += grid[y2][x2];
                    if (x1 > 0 && x2 > 0 && dp[x1 - 1][x2 - 1] >= 0) //from left left
                        best = max(best, dp[x1 - 1][x2 - 1] + delta);
                    if (x1 > 0 && y2 > 0 && dp[x1 - 1][x2] >= 0) //from left up
                        best = max(best, dp[x1 - 1][x2] + delta);
                    if (y1 > 0 && x2 > 0 && dp[x1][x2 - 1] >= 0) //from up left
                        best = max(best, dp[x1][x2 - 1] + delta);
                    if (y1 > 0 && y2 > 0 && dp[x1][x2] >= 0) //from up up
                        best = max(best, dp[x1][x2] + delta);
                    dp[x1][x2] = best;
                }
            }
        }
        return dp[N - 1][N - 1] < 0 ? 0 : dp[N - 1][N - 1];
    }
};
```


