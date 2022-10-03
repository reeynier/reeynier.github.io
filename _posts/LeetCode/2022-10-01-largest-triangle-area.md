---
layout: post
title: "Largest Triangle Area Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Geometry ]
similar: [ Geometry ]
featured: false
hidden: false
excerpt: LeetCode 812. Given an array of points on the X-Y plane points where points[i] = [x_i, y_i], return the area of the largest triangle that can be formed by any three different points. Answers within 10^-5 of the actual answer will be accepted.

---

<br />

## Description

LeetCode Problem 812.

Given an array of points on the X-Y plane points where points[i] = [x_i, y_i], return the area of the largest triangle that can be formed by any three different points. Answers within 10^-5 of the actual answer will be accepted.

Example 1: 
```
Input: points = [[0,0],[0,1],[1,0],[0,2],[2,0]]
Output: 2.00000
Explanation: The five points are shown in the above figure. The red triangle is the largest.
```

Example 2:
```
Input: points = [[1,0],[0,0],[0,1]]
Output: 0.50000
```

Constraints:
* 3 <= points.length <= 50
* -50 <= x_i, y_i <= 50
* All the given points are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    double largestTriangleArea(vector<vector<int>>& points) {
        double ans = 0; 
        for (int i = 0; i < points.size(); ++i) {
            for (int j = i+1; j < points.size(); ++j) {
                for (int k = j+1; k < points.size(); ++k ){
                    double a = sqrt(pow(points[i][0] - points[j][0], 2) + pow(points[i][1] - points[j][1], 2)), 
                    b = sqrt(pow(points[j][0] - points[k][0], 2) + pow(points[j][1] - points[k][1], 2)), 
                    c = sqrt(pow(points[k][0] - points[i][0], 2) + pow(points[k][1] - points[i][1], 2)), 
                    s = (a + b + c)/2; 
                    ans = max(ans, sqrt(s * (s-a) * (s-b) * (s-c)));
                }
            }
        }
        return ans; 
    }
};
```


