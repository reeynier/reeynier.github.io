---
layout: post
title:  "Number of Islands Problem"
categories: [ Algorithm ]
tags: [ Breadth First Search, Queue, Depth First Search, Leetcode ]
similar: [ DFS ]
featured: false
hidden: false
excerpt: LeetCode 200. Given an **m x n** 2d **grid** map of '1's (land) and '0's (water), return the number of islands.
---

<br />

## Description

LeetCode Problem 200. Given an **m x n** 2d **grid** map of '1's (land) and '0's (water), return the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example: 
```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1

Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

<br />

## Solution

#### Breadth First Search

Both the `depth first search` and the `breadth first search` can work for this problem. In this post, we only discuss the breadth first search approach.

We scan through the 2d array. If an element is '1', then we can treat it as a root node that triggers a breadth first search. We put it into a queue and mark it as '0' which means this element has been visited. We then search the four neighborhood elements by putting any elements that are '1's into the queue. We repeat it until the queue becomes empty. 

The time complexity is O(mn).

<br />

## Sample C++ Code


This is a C++ implementation of the breadth first search approach.

```c
#include <iostream>
#include <queue>
#include <algorithm>

using namespace std;

int numIslands(vector<vector<char>>& grid) {
    int m = grid.size();
    if (m == 0) return 0;
    int n = grid[0].size();
    
    int islandsCnt = 0;
    vector<vector<int>> dir = {
        {1,0}, {-1,0}, {0,-1}, {0,1}
    };
    int x, y, r, c;
    for (int i = 0; i < m; i ++) {
        for (int j = 0; j < n; j ++) {
            if (grid[i][j] == '0')
                continue;
            islandsCnt ++;
            
            grid[i][j] = '0';
            
            queue<pair<int, int>> bfsQ;
            bfsQ.push(make_pair(i, j));
            
            while (!bfsQ.empty()) {
                pair<int, int> point = bfsQ.front();
                bfsQ.pop();
                x = point.first, y = point.second;
                grid[x][y] = '0';
                
                // Explore the four neighbors
                for (int k = 0; k < 4; k ++) {
                    r = x + dir[k][0];
                    c = y + dir[k][1];
                    if (r >= 0 && c >= 0 && r < m && c < n && grid[r][c] == '1') {
                        bfsQ.push(make_pair(r, c));
                        // Setting 0 here is important, this will speed up the search
                        // This avoids adding multiple {r,c} pairs to the queue
                        grid[r][c] = '0'; 
                    }
                }
            }
                
        }
    }
    return islandsCnt;
}

int main() {
    vector<vector<char>> grid = {
        {'1','1','0','0','0'},
        {'1','1','0','0','0'},
        {'0','0','1','0','0'},
        {'0','0','0','1','1'}
    };
    cout << numIslands(grid) << endl;
}
```
