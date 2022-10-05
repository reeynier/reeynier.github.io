---
layout: post
title: "Shortest Bridge Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Depth-First Search, Breadth-First Search, Matrix ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 934. You are given an n x n binary matrix grid where 1 represents land and 0 represents water.

---

<br />

## Description

LeetCode Problem 934.

You are given an n x n binary matrix grid where 1 represents land and 0 represents water.

An island is a 4-directionally connected group of 1's not connected to any other 1's. There are exactly two islands in grid.

You may change 0's to 1's to connect the two islands to form one island.

Return the smallest number of 0's you must flip to connect the two islands.

Example 1:
```
Input: grid = [[0,1],[1,0]]
Output: 1
```

Example 2:
```
Input: grid = [[0,1,0],[0,0,0],[0,0,1]]
Output: 2
```

Example 3:
```
Input: grid = [[1,1,1,1,1],[1,0,0,0,1],[1,0,1,0,1],[1,0,0,0,1],[1,1,1,1,1]]
Output: 1
```

Constraints:
* n == grid.length == grid[i].length
* 2 <= n <= 100
* grid[i][j] is either 0 or 1.
* There are exactly two islands in grid.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int dir[5] = {0, 1, 0, -1, 0};
    
    void paint(vector<vector<int>>& A, int i, int j, vector<pair<int, int>> &q) {
        if (min(i, j) >= 0 && max(i, j) < A.size() && A[i][j] == 1) {
            A[i][j] = 2;
            q.push_back({i, j});
            for (int d = 0; d < 4; ++d)
                paint(A, i + dir[d], j + dir[d + 1], q);
        }
    }
    
    int shortestBridge(vector<vector<int>>& A) {
        vector<pair<int, int>> q;
        for (int i = 0; q.size() == 0 && i < A.size(); ++i)
            for (int j = 0; q.size() == 0 && j < A[0].size(); ++j)
                paint(A, i, j, q);
        while (!q.empty()) {
            vector<pair<int, int>> q1;
            for (auto [i, j] : q) {
                for (int d = 0; d < 4; ++d) {
                    int x = i + dir[d], y = j + dir[d + 1];
                    if (min(x, y) >= 0 && max(x, y) < A.size()) {
                        if (A[x][y] == 1)
                            return A[i][j] - 2;
                        if (A[x][y] == 0) {
                            A[x][y] = A[i][j] + 1;
                            q1.push_back({x, y});
                        }
                    }
                }
            }
            swap(q, q1);
        }
        return 0;
    }
};
```


