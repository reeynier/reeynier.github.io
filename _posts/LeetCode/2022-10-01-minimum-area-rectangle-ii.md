---
layout: post
title: "Minimum Area Rectangle II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Geometry ]
similar: [ Geometry ]
featured: false
hidden: false
excerpt: LeetCode 963. You are given an array of points in the X-Y plane points where points[i] = [x_i, y_i].

---

<br />

## Description

LeetCode Problem 963.

You are given an array of points in the X-Y plane points where points[i] = [x_i, y_i].

Return the minimum area of any rectangle formed from these points, with sides not necessarily parallel to the X and Y axes. If there is not any such rectangle, return 0.

Answers within 10^-5 of the actual answer will be accepted.

Example 1: 
```
Input: points = [[1,2],[2,1],[1,0],[0,1]]
Output: 2.00000
Explanation: The minimum area rectangle occurs at [1,2],[2,1],[1,0],[0,1], with an area of 2.
```

Example 2: 
```
Input: points = [[0,1],[2,1],[1,1],[1,0],[2,0]]
Output: 1.00000
Explanation: The minimum area rectangle occurs at [1,0],[1,1],[2,1],[2,0], with an area of 1.
```

Example 3: 
```
Input: points = [[0,3],[1,2],[3,1],[1,3],[2,1]]
Output: 0
Explanation: There is no possible rectangle to form from these points.
```

Example 4: 
```
Input: points = [[3,1],[1,1],[0,1],[2,1],[3,3],[3,2],[0,2],[2,3]]
Output: 2.00000
Explanation: The minimum area rectangle occurs at [2,1],[2,3],[3,3],[3,1], with an area of 2.
```

Constraints:
* 1 <= points.length <= 50
* points[i].length == 2
* 0 <= x_i, y_i <= 4 * 10^4
* All the given points are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:    
    double minAreaFreeRect(vector<vector<int>>& points) {
        long ans = LONG_MAX;
        map<vector<long>, multimap<long, vector<int>>> db;
        
        for (auto i = points.begin(); i != points.end(); i++) {
            for (auto j = i+1; j != points.end(); j++) {
                if (i == j) continue;
                
                long x1 = j->at(0) - i->at(0);
                long y1 = j->at(1) - i->at(1);
                
                long length = x1 * x1 + y1 * y1;
                vector<long> mid = {i->at(0) + j->at(0), i->at(1) + j->at(1)};
                
                if (db.find(mid) == db.end()) {
                    db.insert(std::make_pair(mid, multimap<long, vector<int>>()));
                }
                
                auto &m = (db.find(mid))->second;
                if (m.find(length) != m.end()) {
                    auto p = m.equal_range(length);
                    for (auto k = p.first; k != p.second; k++) {
                        ans = std::min(ans, std::abs(x1 * k->second.at(1) - y1 * k->second.at(0)));
                    }
                }
                m.insert(std::make_pair(length, vector<int>{int(x1), int(y1)}));
            }
        }
        
        return ans == LONG_MAX ? 0 : ans / 2;
    }
};
```


