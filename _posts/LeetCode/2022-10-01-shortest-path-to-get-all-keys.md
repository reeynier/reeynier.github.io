---
layout: post
title: "Shortest Path To Get All Keys Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Bit Manipulation, Breadth-First Search ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 864. You are given an m x n grid grid where

---

<br />

## Description

LeetCode Problem 864.

You are given an m x n grid grid where:
* '.' is an empty cell.
* '#' is a wall.
* '@' is the starting point.
* Lowercase letters represent keys.
* Uppercase letters represent locks.

You start at the starting point and one move consists of walking one space in one of the four cardinal directions. You cannot walk outside the grid, or walk into a wall.

If you walk over a key, you can pick it up and you cannot walk over a lock unless you have its corresponding key.

For some 1 <= k <= 6, there is exactly one lowercase and one uppercase letter of the first k letters of the English alphabet in the grid. This means that there is exactly one key for each lock, and one lock for each key; and also that the letters used to represent the keys and locks were chosen in the same order as the English alphabet.

Return the lowest number of moves to acquire all keys. If it is impossible, return -1.

Example 1: 
```
Input: grid = ["@.a.#","###.#","b.A.B"]
Output: 8
Explanation: Note that the goal is to obtain all the keys not to open all the locks.
```

Example 2: 
```
Input: grid = ["@..aA","..B#.","....b"]
Output: 6
```

Example 3: 
```
Input: grid = ["@Aa"]
Output: -1
```

Constraints:
* m == grid.length
* n == grid[i].length
* 1 <= m, n <= 30
* grid[i][j] is either an English letter, '.', '#', or '@'.
* The number of keys in the grid is in the range [1, 6].
* Each key in the grid is unique.
* Each key in the grid has a matching lock.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int shortestPathAllKeys(vector<string>& grid) {
        int n = grid.size(), m = grid[0].size();
        vector<pair<int, int>> dirs { {0, 1}, {1, 0}, {-1, 0}, {0, -1} };
        queue<tuple<int, int, int>> q;
        bool visited[n + 1][m + 1][(1 << 6) + 1];
        memset(visited, 0, sizeof visited);

        int keys = 0;
        for (int i = 0; i < n; i++) 
            for (int j = 0; j < m; j++) 
                if (grid[i][j] == '@') {
                    // Starting point, Push in queue and mark visited
                    q.push({i, j, 0});
                    visited[i][j][0] = 1; 
                }
                else if (islower(grid[i][j]))
                    keys++;

        int allKeysMask = (1 << keys) - 1, steps = 0;
        while (!q.empty()) {
            int size = q.size();
            while (size--) {
                auto [i, j, currMask] = q.front(); 
                q.pop();
                if (currMask == allKeysMask) 
                    // Got all the keys, return the answer
                    return steps; 

                for (auto &d : dirs) {
                    int r = d.first + i, c = d.second + j;
                    if (r < 0 || c < 0 || r >= n || c >= m || grid[r][c] == '#' || visited[r][c][currMask]) 
                        // Invalid case
                        continue; 
                    if (isupper(grid[r][c]) && !(currMask & (1 << (grid[r][c] - 'A')))) 
                        // Visiting a lock without its corresponding key is an invalid step
                        continue; 

                    int tempMask = currMask;
                    if (islower(grid[r][c])) 
                        // Mark the key as visited in the mask
                        tempMask |= (1 << (grid[r][c] - 'a')); 
                    q.push({r, c, tempMask});
                    visited[r][c][tempMask] = 1;
                }
            }
            steps++;
        }
        return -1;
    }
};
```


