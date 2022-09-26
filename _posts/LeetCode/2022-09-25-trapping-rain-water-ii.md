---
layout: post
title: "Trapping Rain Water II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Breadth-First Search, Heap, Matrix ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 407. Given an m x n integer matrix heightMap representing the height of each unit cell in a 2D elevation map, return the volume of water it can trap after raining.

---

<br />

## Description

LeetCode Problem 407.

Given an m x n integer matrix heightMap representing the height of each unit cell in a 2D elevation map, return the volume of water it can trap after raining.

Example 1: 
```
Input: heightMap = [[1,4,3,1,3,2],[3,2,1,3,2,4],[2,3,3,2,3,1]]
Output: 4
Explanation: After the rain, water is trapped between the blocks.
We have two small ponds 1 and 3 units trapped.
The total volume of water trapped is 4.
```

Example 2: 
```
Input: heightMap = [[3,3,3,3,3],[3,2,2,2,3],[3,2,1,2,3],[3,2,2,2,3],[3,3,3,3,3]]
Output: 10
```

Constraints:
* m == heightMap.length
* n == heightMap[i].length
* 1 <= m, n <= 200
* 0 <= heightMap[i][j] <= 2 * 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int trapRainWater(vector<vector<int>>& heightMap) {
        int m = heightMap.size(), n = (m == 0) ? 0 : heightMap[0].size();        
        if (m < 3 || n < 3) return 0;
        priority_queue<pair<int, pair<int, int>>, vector<pair<int, pair<int, int>>>, greater<pair<int, pair<int, int>>>> pq;
        vector<vector<int>> visited(m, vector<int>(n, 0));
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (!(i == 0 || i == m-1 || j == 0 || j == n-1)) continue;
                pq.push(make_pair(heightMap[i][j], make_pair(i, j)));
                visited[i][j] = 1;
            }
        }
        vector<int> dir = {0, 1, 0, -1, 0};
        int H = INT_MIN;
        int res = 0;
        while (!pq.empty()) {
            auto p = pq.top(); pq.pop();
            int height = p.first, i = p.second.first, j = p.second.second;
            H = max(H, height);
            for (int d = 0; d < 4; d++) {
                int x = i + dir[d], y = j + dir[d+1];
                if (x < 0 || x >= m || y < 0 || y >= n || visited[x][y]) continue;
                visited[x][y] = 1;
                int diff = H - heightMap[x][y];
                if (diff > 0) res += diff;
                pq.push(make_pair(heightMap[x][y], make_pair(x, y)));
            }
        }
        return res;
    } 
};
```


