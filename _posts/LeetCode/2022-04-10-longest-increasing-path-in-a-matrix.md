---
layout: post
title: "Longest Increasing Path In A Matrix Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Depth-First Search, Breadth-First Search, Graph, Topological Sort, Memoization, Matrix ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 329. Given an m x n integers matrix, return the length of the longest increasing path in matrix.

---

<br />

## Description

LeetCode Problem 329.

Given an m x n integers matrix, return the length of the longest increasing path in matrix.
From each cell, you can either move in four directions: left, right, up, or down. You may not move diagonally or move outside the boundary (i.e., wrap-around is not allowed).

Example 1:
```
Input: matrix = [[9,9,4],[6,6,8],[2,1,1]]
Output: 4
Explanation: The longest increasing path is [1, 2, 6, 9].
```

Example 2:
```
Input: matrix = [[3,4,5],[3,2,6],[2,2,1]]
Output: 4
Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.
```

Example 3:
```
Input: matrix = [[1]]
Output: 1
```

Constraints:
* m == matrix.length
* n == matrix[i].length
* 1 <= m, n <= 200
* 0 <= matrix[i][j] <= 2^31 - 1

<br />

## Sample C++ Code

Dynamic programming approach:
* The 2D array dp[i][j] represents the length of longest increasing path starting from (i, j).
* For (i, j) neighbor (i', j'), if matrix[i'][j'] > matrix[i][j] and dp[i'][j'] has been calculated, then calculate dp[i][j] recursively.
* After all dp[i][j] have been calculated, find the maximum dp[i][j].

```c
class Solution {
public:
    int longestIncreasingPath(vector<vector<int>>& matrix) {
        int rows = matrix.size();
        if (!rows) return 0;
        int cols = matrix[0].size();
        
        vector<vector<int>> dp(rows, vector<int>(cols, 0));
        std::function<int(int, int)> dfs = [&] (int x, int y) {
            if (dp[x][y]) return dp[x][y];
            vector<vector<int>> dirs = { {-1, 0}, {1, 0}, {0, 1}, {0, -1} };
            for (auto &dir : dirs) {
                int xx = x + dir[0], yy = y + dir[1];
                if (xx < 0 || xx >= rows || yy < 0 || yy >= cols) continue;
                if (matrix[xx][yy] <= matrix[x][y]) continue;
                dp[x][y] = std::max(dp[x][y], dfs(xx, yy));
            }
            return ++dp[x][y];
        };
        
        int ret = 0;
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < cols; ++j) {
                ret = std::max(ret, dfs(i, j));
            }
        }
        
        return ret;
    }
};
```


