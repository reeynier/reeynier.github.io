---
layout: post
title: "Island Perimeter Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Depth-First Search, Breadth-First Search, Matrix ]
similar: [ Matrix ]
featured: false
hidden: false
excerpt: LeetCode 463. You are given row x col grid representing a map where grid[i][j] = 1 representsland and grid[i][j] = 0 represents water.

---

<br />

## Description

LeetCode Problem 463.

You are given row x col grid representing a map where grid[i][j] = 1 representsland and grid[i][j] = 0 represents water.

Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells).

The island doesn't have "lakes", meaning the water inside isn't connected to the water around the island. One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

Example 1: 
```
Input: grid = [[0,1,0,0],[1,1,1,0],[0,1,0,0],[1,1,0,0]]
Output: 16
Explanation: The perimeter is the 16 yellow stripes in the image above.
```

Example 2:
```
Input: grid = [[1]]
Output: 4
```

Example 3:
```
Input: grid = [[1,0]]
Output: 4
```

Constraints:
* row == grid.length
* col == grid[i].length
* 1 <= row, col <= 100
* grid[i][j] is 0 or 1.
* There is exactly one island in grid.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int islandPerimeter(vector<vector<int>>& grid) {
        if (grid.size() == 0)
            return 0;
        int r = grid.size();
        int c = grid[0].size();
        
        int perim = 0;
        for (int i = 0; i < r; i ++) {
            for  (int j = 0; j < c; j ++) {
                if (grid[i][j] == 1) {
                    if ((i == 0) || (grid[i-1][j] == 0))
                        perim ++;
                    if ((i == r-1) || (grid[i+1][j] == 0))
                        perim ++;
                    if ((j == 0) || (grid[i][j-1] == 0))
                        perim ++;
                    if ((j == c-1) || (grid[i][j+1] == 0))
                        perim ++;
                }
            }
        }
        
        return perim;
    }
};
```


