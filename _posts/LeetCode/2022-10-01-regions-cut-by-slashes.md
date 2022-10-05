---
layout: post
title: "Regions Cut By Slashes Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Depth-First Search, Breadth-First Search, Union Find, Graph ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 959. An n x n grid is composed of 1 x 1 squares where each 1 x 1 square consists of a '/', '\', or blank space ' '. These characters divide the square into contiguous regions.

---

<br />

## Description

LeetCode Problem 959.

An n x n grid is composed of 1 x 1 squares where each 1 x 1 square consists of a '/', '\', or blank space ' '. These characters divide the square into contiguous regions.

Given the grid grid represented as a string array, return the number of regions.

Note that backslash characters are escaped, so a '\' is represented as '\\'.

Example 1: 
```
Input: grid = [" /","/ "]
Output: 2
```

Example 2: 
```
Input: grid = [" /","  "]
Output: 1
```

Example 3: 
```
Input: grid = ["\\/","/\\"]
Output: 4
Explanation: (Recall that because \ characters are escaped, "\\/" refers to \/, and "/\\" refers to /\.)
```

Example 4: 
```
Input: grid = ["/\\","\\/"]
Output: 5
Explanation: (Recall that because \ characters are escaped, "\\/" refers to \/, and "/\\" refers to /\.)
```

Example 5: 
```
Input: grid = ["//","/ "]
Output: 3
```

Constraints:
* n == grid.length
* n == grid[i].length
* 1 <= n <= 30
* grid[i][j] is either '/', '\', or ' '.

<br />

## Sample C++ Code


```c
class Solution {
    void dfs(vector<vector<int>> &grid2, int i , int j){
        if (i < 0 || i >= grid2.size() || j < 0 || j >= grid2[i].size())
            return;
        
        if (grid2[i][j] != 0) 
            return;
        
        grid2[i][j] = 1;
        dfs(grid2, i - 1, j);
        dfs(grid2, i + 1, j);
        dfs(grid2, i, j - 1);
        dfs(grid2, i, j + 1);
    }
public:
    int regionsBySlashes(vector<string>& grid) {
        vector<vector<int>> grid2(grid.size() * 3, vector<int>(grid.size() * 3, 0));
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid[i].size(); j++) {
                if (grid[i][j] == '/') {
                   grid2[i * 3 + 0][j * 3 + 2] = 1;
                   grid2[i * 3 + 1][j * 3 + 1] = 1;
                   grid2[i * 3 + 2][j * 3 + 0] = 1;
                  } else if (grid[i][j] == '\\') {
                   grid2[i * 3 + 0][j * 3 + 0] = 1;
                   grid2[i * 3 + 1][j * 3 + 1] = 1;
                   grid2[i * 3 + 2][j * 3 + 2] = 1;
                }
            }
        }
        int ans = 0;
        for (int i = 0; i < grid2.size(); i++) {
            for (int j = 0; j < grid2[i].size(); j++) {
                if (grid2[i][j] == 0) {
                    dfs(grid2, i, j);
                    ans++;
                }
            }
        }
        return ans;
    }
};
```


