---
layout: post
title: "Minimum Area Rectangle Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Math, Geometry, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 939. You are given an array of points in the X-Y plane points where points[i] = [x_i, y_i].

---

<br />

## Description

LeetCode Problem 939.

You are given an array of points in the X-Y plane points where points[i] = [x_i, y_i].

Return the minimum area of a rectangle formed from these points, with sides parallel to the X and Y axes. If there is not any such rectangle, return 0.

Example 1: 
```
Input: points = [[1,1],[1,3],[3,1],[3,3],[2,2]]
Output: 4
```

Example 2: 
```
Input: points = [[1,1],[1,3],[3,1],[3,3],[4,1],[4,3]]
Output: 2
```

Constraints:
* 1 <= points.length <= 500
* points[i].length == 2
* 0 <= x_i, y_i <= 4 * 10^4
* All the given points are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int minAreaRect(vector<vector<int>>& points) {
        int ans = INT_MAX;
        unordered_map<int, unordered_set<int>> m;
        
        for (auto p : points) {
            m[p[0]].insert(p[1]);
        }
        
        /*
            A ----------------------------D
            |(x1, y1)             (x2, y1)|
            |                             |
            |(x1, y2)             (x2, y2)|  
            C ----------------------------B
        */
        for (int i = 0; i < points.size(); i++) {
            for (int j = i+1; j < points.size(); j++) {
                int x1 = points[i][0];  // A
                int y1 = points[i][1];  // A
                int x2 = points[j][0];  // B
                int y2 = points[j][1];  //B
                
                if ((x1 != x2) && (y2 != y1)) { // diagonal
                    if (m[x1].find(y2) != m[x1].end() && m[x2].find(y1) != m[x2].end()) { // C & D
                        ans = min(ans, (abs(x1-x2) * abs(y1-y2)));
                    }
                }
            }
        }

        return ((ans == INT_MAX) ? 0 : ans);
    }
};
```


