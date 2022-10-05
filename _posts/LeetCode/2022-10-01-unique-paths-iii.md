---
layout: post
title: "Unique Paths III Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Backtracking, Bit Manipulation, Matrix ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 980. You are given an m x n integer array grid where grid[i][j] could be

---

<br />

## Description

LeetCode Problem 980.

You are given an m x n integer array grid where grid[i][j] could be:
* 1 representing the starting square. There is exactly one starting square.
* 2 representing the ending square. There is exactly one ending square.
* 0 representing empty squares we can walk over.
* -1 representing obstacles that we cannot walk over.

Return the number of 4-directional walks from the starting square to the ending square, that walk over every non-obstacle square exactly once.

Example 1: 
```
Input: grid = [[1,0,0,0],[0,0,0,0],[0,0,2,-1]]
Output: 2
Explanation: We have the following two paths: 
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2)
2. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2)
```

Example 2: 
```
Input: grid = [[1,0,0,0],[0,0,0,0],[0,0,0,2]]
Output: 4
Explanation: We have the following four paths: 
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2),(2,3)
2. (0,0),(0,1),(1,1),(1,0),(2,0),(2,1),(2,2),(1,2),(0,2),(0,3),(1,3),(2,3)
3. (0,0),(1,0),(2,0),(2,1),(2,2),(1,2),(1,1),(0,1),(0,2),(0,3),(1,3),(2,3)
4. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2),(2,3)
```

Example 3: 
```
Input: grid = [[0,1],[2,0]]
Output: 0
Explanation: There is no path that walks over every empty square exactly once.
Note that the starting and ending square can be anywhere in the grid.
```

Constraints:
* m == grid.length
* n == grid[i].length
* 1 <= m, n <= 20
* 1 <= m * n <= 20
* -1 <= grid[i][j] <= 2
* There is exactly one starting cell and one ending cell.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int paths;
    
    void dfs(vector<vector<int>> &grid, int x, int y, int cntzero) {
        if (x < 0 || x >= grid.size() || y < 0 || y >= grid[0].size())
            return;

        if (grid[x][y] == 1 || grid[x][y] == -1 || cntzero < 0) 
            return;
        if (grid[x][y] == 2) {
            if (cntzero == 0)
                paths ++;
            return;
        }
        
        grid[x][y] = -1;
        
        dfs(grid, x-1, y, cntzero-1);
        dfs(grid, x+1, y, cntzero-1);
        dfs(grid, x, y-1, cntzero-1);
        dfs(grid, x, y+1, cntzero-1);
        
        grid[x][y] = 0;
        
    }
    
    int uniquePathsIII(vector<vector<int>>& grid) {
        paths = 0;
        int r = grid.size(), c = grid[0].size();
        
        int cntzero = 0;
        int starti, startj;
        for (int i = 0; i < r; i ++) {
            for (int j = 0; j < c; j ++) {
                if (grid[i][j] == 1) {
                    starti = i, startj = j;
                } else if (grid[i][j] == 0) {
                    cntzero ++;
                }
            }
        }
        
        dfs(grid, starti-1, startj, cntzero);
        dfs(grid, starti+1, startj, cntzero);
        dfs(grid, starti, startj-1, cntzero);
        dfs(grid, starti, startj+1, cntzero);
        return paths;
    }
};
```


