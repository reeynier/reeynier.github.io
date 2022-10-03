---
layout: post
title: "Making A Large Island Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Depth-First Search, Breadth-First Search, Union Find, Matrix ]
similar: [ Matrix ]
featured: false
hidden: false
excerpt: LeetCode 827. You are given an n x n binary matrix grid. You are allowed to change at most one 0 to be 1.

---

<br />

## Description

LeetCode Problem 827.

You are given an n x n binary matrix grid. You are allowed to change at most one 0 to be 1.
Return the size of the largest island in grid after applying this operation.

An island is a 4-directionally connected group of 1s.

Example 1:
```
Input: grid = [[1,0],[0,1]]
Output: 3
Explanation: Change one 0 to 1 and connect two 1s, then we get an island with area = 3.
```

Example 2:
```
Input: grid = [[1,1],[1,0]]
Output: 4
Explanation: Change the 0 to 1 and make the island bigger, only one island with area = 4.
```

Example 3:
```
Input: grid = [[1,1],[1,1]]
Output: 4
Explanation: Can't change any 0 to 1, only one island with area = 4.
```

Constraints:
* n == grid.length
* n == grid[i].length
* 1 <= n <= 500
* grid[i][j] is either 0 or 1.

<br />

## Sample C++ Code


```c
class Solution {
public:
    const int DIR[5] = {0, 1, 0, -1, 0};
    int m, n;
    unordered_map<int, int> componentSize;
    int largestIsland(vector<vector<int>>& grid) {
        m = grid.size(); n = grid[0].size();
        int ans = 0, nextColor = 2;
        for (int r = 0; r < m; ++r) {
            for (int c = 0; c < n; ++c) {
                if (grid[r][c] != 1) continue; // Only paint when it's an island cell
                paint(grid, r, c, nextColor++);
                ans = max(ans, componentSize[nextColor - 1]);
            }
        }
        for (int r = 0; r < m; ++r) {
            for (int c = 0; c < n; ++c) {
                if (grid[r][c] != 0) continue; // Skip non-empty cell
                unordered_set<int> neighborColors;
                for (int i = 0; i < 4; ++i) {
                    int nr = r + DIR[i], nc = c + DIR[i+1];
                    if (nr < 0 || nr == m || nc < 0 || nc == n || grid[nr][nc] == 0) 
                        continue;
                    neighborColors.insert(grid[nr][nc]);
                }
                int sizeFormed = 1;
                for (int color : neighborColors) 
                    sizeFormed += componentSize[color];
                ans = max(ans, sizeFormed);
            }
        }
        return ans;
    }
    void paint(vector<vector<int>>& grid, int r, int c, int color) {
        if (r < 0 || r == m || c < 0 || c == n || grid[r][c] != 1) 
            return;
        grid[r][c] = color;
        componentSize[color] += 1;
        for (int i = 0; i < 4; ++i) 
            paint(grid, r + DIR[i], c + DIR[i+1], color);
    }
};
```


