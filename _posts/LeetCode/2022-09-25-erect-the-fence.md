---
layout: post
title: "Erect The Fence Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Geometry ]
similar: [ Geometry ]
featured: false
hidden: false
excerpt: LeetCode 587. You are given an array trees where trees[i] = [x_i, y_i] represents the location of a tree in the garden.

---

<br />

## Description

LeetCode Problem 587.

You are given an array trees where trees[i] = [x_i, y_i] represents the location of a tree in the garden.

You are asked to fence the entire garden using the minimum length of rope as it is expensive. The garden is well fenced only if all the trees are enclosed.

Return the coordinates of trees that are exactly located on the fence perimeter.

Example 1: 
```
Input: points = [[1,1],[2,2],[2,0],[2,4],[3,3],[4,2]]
Output: [[1,1],[2,0],[3,3],[2,4],[4,2]]
```

Example 2: 
```
Input: points = [[1,2],[2,2],[4,2]]
Output: [[4,2],[2,2],[1,2]]
```

Constraints:
* 1 <= points.length <= 3000
* points[i].length == 2
* 0 <= x_i, y_i <= 100
* All the given points are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<vector<int>> outerTrees(vector<vector<int>>& points) {
        // Monotone chain method
        int n = points.size();
        vector<vector<int>> ans;
        sort(points.begin(), points.end(), mycompare);
        // left to right
        for (int i = 0; i < n; ++i) {
            while (ans.size() > 1 && orientation(ans[ans.size()-2], ans.back(), points[i]) < 0) 
                ans.pop_back();
            ans.push_back(points[i]);
        }
        // if all points along a line, ans.size() is n after left to right procedure
        if (ans.size() == n) return ans;
        // right to left
        for (int i = n-2; i >= 0; --i) {
            while (ans.size() > 1 && orientation(ans[ans.size()-2], ans.back(), points[i]) < 0) 
                ans.pop_back();
            ans.push_back(points[i]);
        }
        ans.pop_back();
        return ans;
    }
    static bool mycompare(vector<int>& a, vector<int>& b) {
        return a[0] < b[0] || (a[0] == b[0] && a[1] < b[1]);
    }
    int orientation(vector<int>& a, vector<int>& b, vector<int>& c) {
        return (b[0] - a[0])*(c[1] - b[1]) - (b[1] - a[1])*(c[0] - b[0]);
    }
};
```


