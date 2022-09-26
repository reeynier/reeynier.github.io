---
layout: post
title: "Contain Virus Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Depth-First Search, Breadth-First Search, Matrix ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 749. A virus is spreading rapidly, and your task is to quarantine the infected area by installing walls.

---

<br />

## Description

LeetCode Problem 749.

A virus is spreading rapidly, and your task is to quarantine the infected area by installing walls.

The world is modeled as an m x n binary grid isInfected, where isInfected[i][j] == 0 represents uninfected cells, and isInfected[i][j] == 1 represents cells contaminated with the virus. A wall (and only one wall) can be installed between any two 4-directionally adjacent cells, on the shared boundary.

Every night, the virus spreads to all neighboring cells in all four directions unless blocked by a wall. Resources are limited. Each day, you can install walls around only one region (i.e., the affected area (continuous block of infected cells) that threatens the most uninfected cells the following night). There will never be a tie.

Return the number of walls used to quarantine all the infected regions. If the world will become fully infected, return the number of walls used.

Example 1: 
```
Input: isInfected = [[0,1,0,0,0,0,0,1],[0,1,0,0,0,0,0,1],[0,0,0,0,0,0,0,1],[0,0,0,0,0,0,0,0]]
Output: 10
Explanation: There are 2 contaminated regions.
On the first day, add 5 walls to quarantine the viral region on the left. The board after the virus spreads is:
<img alt="" src="https://assets.leetcode.com/uploads/2021/06/01/virus12edited-grid.jpg" style="width: 500px; height: 257px;" />
On the second day, add 5 walls to quarantine the viral region on the right. The virus is fully contained.
<img alt="" src="https://assets.leetcode.com/uploads/2021/06/01/virus13edited-grid.jpg" style="width: 500px; height: 261px;" />
```

Example 2: 
```
Input: isInfected = [[1,1,1],[1,0,1],[1,1,1]]
Output: 4
Explanation: Even though there is only one cell saved, there are 4 walls built.
Notice that walls are only built on the shared boundary of two different cells.
```

Example 3:
```
Input: isInfected = [[1,1,1,0,0,0,0,0,0],[1,0,1,0,1,1,1,1,1],[1,1,1,0,0,0,0,0,0]]
Output: 13
Explanation: The region on the left only builds two new walls.
```

Constraints:
* m ==isInfected.length
* n ==isInfected[i].length
* 1 <= m, n <= 50
* isInfected[i][j] is either 0 or 1.
* There is always a contiguous viral region throughout the described process that will infect strictly more uncontaminated squares in the next round.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int containVirus(vector<vector<int>>& grid) {
        int ans = 0;
        while (true) {
            int walls = model(grid);
            if (walls == 0) break;
            ans += walls;
        }
        return ans;
    }
private:
    int model(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size(), N = 100;
        vector<unordered_set<int>> virus, toInfect;
        vector<vector<int>> visited(m, vector<int>(n, 0));
        vector<int> walls;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1 && visited[i][j] == 0) {
                    virus.push_back(unordered_set<int>());
                    toInfect.push_back(unordered_set<int>());
                    walls.push_back(0);
                    dfs(grid, visited, virus.back(), toInfect.back(), walls.back(), i, j);
                }
            }
        }
        int maxArea = 0, idx = -1;
        for (int i = 0; i < toInfect.size(); i++) {
            if (toInfect[i].size() > maxArea) {
                maxArea = toInfect[i].size();
                idx = i;
            }
        }
        if (idx == -1) return 0;
        for (int i = 0; i < toInfect.size(); i++) {
            if (i != idx) {
                for (int key : toInfect[i]) 
                    grid[key/N][key%N] = 1;
            }
            else {
                for (int key: virus[i]) 
                    grid[key/N][key%N] = -1;
            }
        }
        return walls[idx];
    }
private:
    void dfs(vector<vector<int>>& grid, vector<vector<int>>& visited, unordered_set<int>& virus, unordered_set<int>& toInfect, int& wall, int row, int col) {
        int m = grid.size(), n = grid[0].size(), N = 100;
        if (row < 0 || row >= m || col < 0 || col >= n || visited[row][col] == 1) return;
        if (grid[row][col] == 1) {
            visited[row][col] = 1;
            virus.insert(row*N + col);
            vector<int> dir = {0, -1, 0, 1, 0};
            for (int i = 0; i < 4; i++)
                dfs(grid, visited, virus, toInfect, wall, row+dir[i], col+dir[i+1]);
        }
        else if (grid[row][col] == 0) {
            wall++;
            toInfect.insert(row*N + col);
        }
    }
};
```


