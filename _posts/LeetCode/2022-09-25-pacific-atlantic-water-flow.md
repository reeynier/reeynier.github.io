---
layout: post
title: "Pacific Atlantic Water Flow Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Depth-First Search, Breadth-First Search, Matrix ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 417. There is an m x n rectangular island that borders both the Pacific Ocean and Atlantic Ocean. The Pacific Ocean touches the island's left and top edges, and the Atlantic Ocean touches the island's right and bottom edges.

---

<br />

## Description

LeetCode Problem 417.

There is an m x n rectangular island that borders both the Pacific Ocean and Atlantic Ocean. The Pacific Ocean touches the island's left and top edges, and the Atlantic Ocean touches the island's right and bottom edges.

The island is partitioned into a grid of square cells. You are given an m x n integer matrix heights where heights[r][c] represents the height above sea level of the cell at coordinate (r, c).

The island receives a lot of rain, and the rain water can flow to neighboring cells directly north, south, east, and west if the neighboring cell's height is less than or equal to the current cell's height. Water can flow from any cell adjacent to an ocean into the ocean.

Return a 2D list of grid coordinates result where result[i] = [r_i, c_i] denotes that rain water can flow from cell (r_i, c_i) to both the Pacific and Atlantic oceans.

Example 1: 
```
Input: heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
```

Example 2:
```
Input: heights = [[2,1],[1,2]]
Output: [[0,0],[0,1],[1,0],[1,1]]
```

Constraints:
* m == heights.length
* n == heights[r].length
* 1 <= m, n <= 200
* 0 <= heights[r][c] <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    void bfs(vector<vector<int>>& matrix, map<pair<int,int>, int>& ocean, 
            queue<pair<int, int>>& oceanQ) {
        int row = matrix.size();
        int col = matrix[0].size();
        
        int dir[4][2] = { {1, 0}, {-1, 0}, {0, 1}, {0, -1} };
        while (!oceanQ.empty()) {
            pair<int, int> curr = oceanQ.front();
            oceanQ.pop();
            for (int i = 0; i < 4; i ++) {
                int new_r = curr.first + dir[i][0];
                int new_c = curr.second + dir[i][1];
                if ((new_r >= 0) && (new_r < row) && (new_c >= 0) && (new_c < col)) {
                    if (matrix[new_r][new_c] >= matrix[curr.first][curr.second]) {
                        if (ocean.find({new_r, new_c}) == ocean.end()) {
                            oceanQ.push({new_r, new_c});
                            ocean[{new_r, new_c}] = 1;
                        }
                    }
                }
            }
        }
        
        return;
    }
    
    vector<vector<int>> pacificAtlantic(vector<vector<int>>& matrix) {
        map<pair<int,int>, int> pacific, atlantic;
        
        if (matrix.size() == 0)
            return matrix;
        int row = matrix.size();
        int col = matrix[0].size();
        
        queue<pair<int, int>> pacificQ, atlanticQ;
        
        for (int i = 0; i < row; i ++) {
            pacificQ.push({i, 0});
            pacific[{i, 0}] = 1;
            atlanticQ.push({i, col-1});
            atlantic[{i, col-1}] = 1;
        }
        for (int j = 0; j < col; j ++) {
            pacificQ.push({0, j});
            pacific[{0, j}] = 1;
            atlanticQ.push({row-1, j});
            atlantic[{row-1, j}] = 1;
        }
        
        bfs(matrix, pacific, pacificQ);
        bfs(matrix, atlantic, atlanticQ);
        
        vector<vector<int>> ans;
        for (map<pair<int, int>, int>::iterator mit = pacific.begin(); 
            mit != pacific.end(); mit ++) {
            if (atlantic.find(mit->first) != atlantic.end()) {
                ans.push_back({mit->first.first, mit->first.second});
            }
        }
        return ans;
    }
};
```


