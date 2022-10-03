---
layout: post
title: "Rotting Oranges Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Breadth-First Search, Matrix ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 994. You are given an m x n grid where each cell can have one of three values

---

<br />

## Description

LeetCode Problem 994.

You are given an m x n grid where each cell can have one of three values:
* 0 representing an empty cell,
* 1 representing a fresh orange, or
* 2 representing a rotten orange.

Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.

Example 1: 
```
Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4
```

Example 2:
```
Input: grid = [[2,1,1],[0,1,1],[1,0,1]]
Output: -1
Explanation: The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.
```

Example 3:
```
Input: grid = [[0,2]]
Output: 0
Explanation: Since there are already no fresh oranges at minute 0, the answer is just 0.
```

Constraints:
* m == grid.length
* n == grid[i].length
* 1 <= m, n <= 10
* grid[i][j] is 0, 1, or 2.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
       queue<pair<int,int>> bfs;
        int count_zeroes = 0;
        int rows = grid.size();
        int cols = grid[0].size();
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid[0].size(); j++) {
                if (grid[i][j] == 2) {
                    bfs.push({i, j});
                }
                else if (grid[i][j] == 0) {
                    ++count_zeroes;
                }
            }
        }
        int oranges = (rows * cols) - count_zeroes;
        int num_el = bfs.size();
        int minutes = 0;
        while (num_el < oranges && !bfs.empty()) {
            ++minutes;
            int n = bfs.size();
            for (int i = 0; i < n; i++) {
                int r = bfs.front().first;
                int c = bfs.front().second;
                bfs.pop();
                if (r > 0 && grid[r - 1][c] == 1) {
                    bfs.push({r - 1, c});
                    grid[r - 1][c] = 2;
                }
                if (r < rows - 1 && grid[r + 1][c] == 1) {
                    bfs.push({r + 1, c});
                    grid[r + 1][c] = 2;
                }
                if (c > 0 && grid[r][c-1] == 1) {
                    bfs.push({r, c - 1});
                    grid[r][c - 1] = 2;
                }
                if (c < cols - 1 && grid[r][c + 1] == 1) {
                    bfs.push({r, c + 1});
                    grid[r][c + 1] = 2;
                }
            }
            num_el += bfs.size();
            if (num_el == oranges) 
                return minutes;
        }
        if (num_el < oranges) 
            return -1;
        return minutes;
    }
};
```


