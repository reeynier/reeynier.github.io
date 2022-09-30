---
layout: post
title: "Bricks Falling When Hit Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Union Find, Matrix ]
similar: [ Matrix ]
featured: false
hidden: false
excerpt: LeetCode 803. You are given an m x n binary grid, where each 1 represents a brick and 0 represents an empty space.

---

<br />

## Description

LeetCode Problem 803.

You are given an m x n binary grid, where each 1 represents a brick and 0 represents an empty space. A brick is stable if:
* It is directly connected to the top of the grid, or
* At least one other brick in its four adjacent cells is stable.

You are also given an array hits, which is a sequence of erasures we want to apply. Each time we want to erase the brick at the location hits[i] = (row_i, col_i). The brick on that location(if it exists) will disappear. Some other bricks may no longer be stable because of that erasure and will fall. Once a brick falls, it is immediately erased from the grid (i.e., it does not land on other stable bricks).

Return an array result, where each result[i] is the number of bricks that will fall after the i^th erasure is applied.

Note that an erasure may refer to a location with no brick, and if it does, no bricks drop.

Example 1:
```
Input: grid = [[1,0,0,0],[1,1,1,0]], hits = [[1,0]]
Output: [2]
Explanation: Starting with the grid:
[[1,0,0,0],
[1,1,1,0]]
We erase the underlined brick at (1,0), resulting in the grid:
[[1,0,0,0],
[0,1,1,0]]
The two underlined bricks are no longer stable as they are no longer connected to the top nor adjacent to another stable brick, so they will fall. The resulting grid is:
[[1,0,0,0],
[0,0,0,0]]
Hence the result is [2].
```

Example 2:
```
Input: grid = [[1,0,0,0],[1,1,0,0]], hits = [[1,1],[1,0]]
Output: [0,0]
Explanation: Starting with the grid:
[[1,0,0,0],
[1,1,0,0]]
We erase the underlined brick at (1,1), resulting in the grid:
[[1,0,0,0],
[1,0,0,0]]
All remaining bricks are still stable, so no bricks fall. The grid remains the same:
[[1,0,0,0],
[1,0,0,0]]
Next, we erase the underlined brick at (1,0), resulting in the grid:
[[1,0,0,0],
[0,0,0,0]]
Once again, all remaining bricks are still stable, so no bricks fall.
Hence the result is [0,0].
```

Constraints:
* m == grid.length
* n == grid[i].length
* 1 <= m, n <= 200
* grid[i][j] is 0 or 1.
* 1 <= hits.length <= 4 * 10^4
* hits[i].length == 2
* 0 <= x_i<= m - 1
* 0 <=y_i <= n - 1
* All (x_i, y_i) are unique.

<br />

## Sample C++ Code


```c
class Solution {
    const vector<pair<int, int>> directions{ {1, 0}, {-1, 0}, {0, 1}, {0, -1} };
    static constexpr int CEILING_ROW = 0;
    
    int dfs(vector<vector<int>>& grid, const int row, const int col) {
        // Return num bricks attached to ceiling.
        // Also floodfill to mark cells connected to ceiling already "2"
        
        // base
        if (row < 0 || col < 0 || row >= grid.size() || col >= grid[0].size())
            return 0;        
        if (grid[row][col] != 1)
            return 0;
        
        grid[row][col] = 2; // 2 means brick in a cluster connected to ceiling  
        int ans = 1;        // At least this brick. 
        for (const auto [dx, dy] : directions)
            ans += dfs(grid, row+dx, col + dy);
        
        return ans;
    }
    
public:
    vector<int> hitBricks(vector<vector<int>>& grid, vector<vector<int>>& hits) {
        // Instead of we count fallen ones after each cut, 
        // we reverse the process by first removing all the hits. 
        // Count how many connected components from ceiling 
        // (no need to worry about bricks getting hold up by other ceiling-connected ones)
        // and find the difference each time we add back a brick which was hit.
        
        // First remove brick according to hits
        for (const auto & hit : hits)
            grid[hit[0]][hit[1]] = grid[hit[0]][hit[1]]? 0: -1; // -1 means hitting a blank spot. 
        
        vector<int> ans(hits.size(), 0); 
        
        // Initial condition after all hit ones removed.
        for (int col = 0; col < grid[0].size(); ++col)
            dfs(grid, CEILING_ROW, col);
        
        for (int i = hits.size() -1; i >=0; --i) {
            const int row = hits[i][0], col = hits[i][1];

            // everytime we add a brick, we probe if
            //  - it's attached to a ceiling-connected cluster, by checking its 4 neighbors
            //  - or it's directly attached to ceiling.
            // if either, we have to perform DFS again to recount how many bricks can be connected to ceiling. 
            int & hit_spot = grid[row][col];
            if (hit_spot == -1)
                // ignore as it was an empty spot.
                continue;
            
            hit_spot = 1;
            
            // Recount condition 1: attached to ceiling directly.
            bool needs_to_recount = (row == CEILING_ROW);            
            if (!needs_to_recount) {
                for (const auto [dx, dy] : directions) {
                    if (row + dx  < 0 || col + dy < 0 || row + dx >= grid.size() || col + dy >= grid[0].size())
                        continue;
                                        
                    if (grid[row+dx][col+dy] == 2)
                        // Recount condition 2: one neighbor can reach ceiling.
                        needs_to_recount = true;
                }
            }
            
            if (needs_to_recount)
                ans[i] = dfs(grid, row, col) - 1; // Exclude the newly added back one. 
        }
        
        return ans;        
    }
};
```


