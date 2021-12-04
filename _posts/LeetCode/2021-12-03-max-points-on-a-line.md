---
layout: post
title: "Max Points On A Line Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Math, Geometry ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 149. Given an array of points where points[i] = [x_i, y_i] represents a point on the X-Y plane, return the maximum number of points that lie on the same straight line.

---

<br />

## Description

LeetCode Problem 149.

Given an array of points where points[i] = [x_i, y_i] represents a point on the X-Y plane, return the maximum number of points that lie on the same straight line.

Example 1: 
```
Input: points = [[1,1],[2,2],[3,3]]
Output: 3
```

Example 2: 
```
Input: points = [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
Output: 4
```

Constraints:
* 1 <= points.length <= 300
* points[i].length == 2
* -10^4 <= x_i, y_i <= 10^4
* All the points are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maxPoints(vector<vector<int>>& points) {
        int result = 0;
        for(int i=0; i<points.size(); ++i) {
            unordered_map<long double,int> h;
            int same = 1;
            int localmax = 0;
            for(int j=i+1; j<points.size(); ++j){ 
                if(points[i][0] == points[j][0] && points[i][1]==points[j][1]){
                    same++;
                }
                else if(points[i][0]==points[j][0]){
                    h[INT_MAX]++;
                }
                else {
                    long double slope = (long double)(points[i][1] - points[j][1]) / 
                    		(long double)(points[i][0] - points[j][0]);
                    h[slope]++;
                }
            }
            for(auto i : h) {
                localmax = max(localmax,i.second);
            }
            localmax +=same;
            result = max(result,localmax);
        }
        return result;
    }
};
```


