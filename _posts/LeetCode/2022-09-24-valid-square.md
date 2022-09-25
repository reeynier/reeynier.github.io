---
layout: post
title: "Valid Square Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Geometry ]
similar: [ Geometry ]
featured: false
hidden: false
excerpt: LeetCode 593. Given the coordinates of four points in 2D space p1, p2, p3 and p4, return true if the four points construct a square.

---

<br />

## Description

LeetCode Problem 593.

Given the coordinates of four points in 2D space p1, p2, p3 and p4, return true if the four points construct a square.

The coordinate of a point p_i is represented as [x_i, y_i]. The input is not given in any order.

A valid square has four equal sides with positive length and four equal angles (90-degree angles).

Example 1:
```
Input: p1 = [0,0], p2 = [1,1], p3 = [1,0], p4 = [0,1]
Output: true
```

Example 2:
```
Input: p1 = [0,0], p2 = [1,1], p3 = [1,0], p4 = [0,12]
Output: false
```

Example 3:
```
Input: p1 = [1,0], p2 = [-1,0], p3 = [0,1], p4 = [0,-1]
Output: true
```

Constraints:
* p1.length == p2.length == p3.length == p4.length == 2
* -10^4 <= x_i, y_i <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    // helper function to calculate distance between two points
    double dist(vector<int>& p1, vector<int>& p2) {
        return sqrt((p2[0] - p1[0]) * (p2[0] - p1[0]) + (p2[1] - p1[1]) * (p2[1] - p1[1]));
    }
    
    bool validSquare(vector<int>& p1, vector<int>& p2, vector<int>& p3, vector<int>& p4) {
        // keep points in an array to be able to get them by index
        vector<vector<int>> points = {p1, p2, p3, p4};
        set<double> lengths;
        
        for (int i=0; i<4; i++) {
            for (int j=i+1; j<4; j++) {
                double curr = dist(points[i], points[j]);
                if (curr != 0)
                    lengths.insert(curr);
                
                // if distance is zero - we got a duplicated point
                else
                    return false;
            }
        }
        // We are supposed to end with only two different lengths: the sides and the diagonals
        return lengths.size() == 2;
    }
};
```


