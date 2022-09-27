---
layout: post
title: "Cut Off Trees For Golf Event Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Breadth-First Search, Heap, Matrix ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 675. You are asked to cut off all the trees in a forest for a golf event. The forest is represented as an m x n matrix. 

---

<br />

## Description

LeetCode Problem 675.

You are asked to cut off all the trees in a forest for a golf event. The forest is represented as an m x n matrix. In this matrix:
* 0 means the cell cannot be walked through.
* 1 represents an empty cell that can be walked through.
* A number greater than 1 represents a tree in a cell that can be walked through, and this number is the tree's height.

In one step, you can walk in any of the four directions: north, east, south, and west. If you are standing in a cell with a tree, you can choose whether to cut it off.

You must cut off the trees in order from shortest to tallest. When you cut off a tree, the value at its cell becomes 1 (an empty cell).

Starting from the point (0, 0), return the minimum steps you need to walk to cut off all the trees. If you cannot cut off all the trees, return -1.

You are guaranteed that no two trees have the same height, and there is at least one tree needs to be cut off.

Example 1: 
```
Input: forest = [[1,2,3],[0,0,4],[7,6,5]]
Output: 6
Explanation: Following the path above allows you to cut off the trees from shortest to tallest in 6 steps.
```

Example 2: 
```
Input: forest = [[1,2,3],[0,0,0],[7,6,5]]
Output: -1
Explanation: The trees in the bottom row cannot be accessed as the middle row is blocked.
```

Example 3:
```
Input: forest = [[2,3,4],[0,0,5],[8,7,6]]
Output: 6
Explanation: You can follow the same path as Example 1 to cut off all the trees.
Note that you can cut off the first tree at (0, 0) before making any steps.
```

Constraints:
* m == forest.length
* n == forest[i].length
* 1 <= m, n <= 50
* 0 <= forest[i][j] <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    int cutOffTree(vector<vector<int>>& forest) {
        int rows = forest.size();
        int cols = rows ? forest[0].size() : 0;
        
        if (!rows || !cols) {
            return 0;
        }
        // Start location is blocked
        if (forest[0][0] == 0) {
            return -1;
        }
        
        // Min queue of trees based on height
         priority_queue<pair<int, pair<int, int>>, vector<pair<int, pair<int, int>>>, greater<pair<int, pair<int, int>>>> trees;
        
        for (int r = 0; r < rows; ++r) {
            for (int c = 0; c < cols; ++c) {
                if (forest[r][c] > 1) {
                   trees.push({forest[r][c], {r, c}}); 
                }
            }
        }
        
        // Legal moves
        vector<pair<int, int>> moves = { {-1, 0}, {1, 0}, {0, -1}, {0, 1} };
        // Track visited
        vector<vector<int>> visited(rows, vector<int>(cols, -1));
        // Total distance
        int totalDist = 0;
        // Start location
        pair<int, int> start = {0, 0};
        // Tree ID
        int i = 0;
        
        // Iterate through trees in increasing height order
        while (!trees.empty()) {
            pair<int, int> to = trees.top().second;
            trees.pop();
            
            // Level order traversal
            bool found = false;
            int dist = -1;  
            queue<pair<int, int>> qu;
            
            qu.push({start.first, start.second});
            visited[start.first][start.second] = i;
            
            while (!qu.empty() && !found) {
                ++dist;
                
                for (int j = 0, r, c, size = qu.size(); j < size && !found; ++j) {
                    tie(r, c) = qu.front();
                    qu.pop();
                
                    // Break if target location found
                    if (r == to.first && c == to.second) {
                        found = true;
                        break;
                    }
                
                    for (int m = 0, nr, nc; m < 4; ++m) {
                        // New location
                        nr = r + moves[m].first;
                        nc = c + moves[m].second;

                        // Skip out of bound, blockages and already scheduled
                        if (nr < 0 || nr >= rows || nc < 0 || nc >= cols || visited[nr][nc] == i || forest[nr][nc] == 0) {
                            continue;
                        }
                            
                        // Mark visited asap otherwise it will be scheduled mutiple times
                        visited[nr][nc] = i;
                        qu.push({nr, nc});
                    }
                }
            }
            
            // Return if not found
            if (!found) {
                return -1;
            }
            
            // Update total distance
            totalDist += dist;
            // Update start
            start = to;
            // Update id
            ++i;
        }
        
        return totalDist;
    }
};

```


