---
layout: post
title:  "Spiral Matrix Problem"
categories: [ Data Structure ]
tags: [ Array, Matrix, Leetcode ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 54. Given an m x n matrix, return all elements of the matrix in spiral order. 
---

<br />

## Description

LeetCode Problem 54. 

Given an m x n matrix, return all elements of the matrix in spiral order. 

Example 1:
```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

Example 2:
```
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

Constraints:

* m == matrix.length
* n == matrix[i].length
* 1 <= m, n <= 10
* -100 <= matrix[i][j] <= 100


<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> ans;
        int m = matrix.size();
        if (m == 0) return ans;
        int n = matrix[0].size();
        
        vector<vector<int>> dir = { {0,1}, {1,0}, {0,-1}, {-1, 0} };
        int diff = 0, turns = 0, i = 0;
        int x = 0, y = 0;
        
        while (i < m*n) {
            ans.push_back(matrix[x][y]);
            if ((turns%4 == 0 && y+diff >= n-1) ||
                (turns%4 == 1 && x+diff >= m-1) || 
                (turns%4 == 2 && y-diff <= 0) || 
                (turns%4 == 3 && x-diff <= 0)){ 
                turns ++;
                if (turns%4 == 3)
                    diff ++;
            }
            x += dir[turns%4][0];
            y += dir[turns%4][1];
            i ++;
        }
        return ans;
    }
};
```
