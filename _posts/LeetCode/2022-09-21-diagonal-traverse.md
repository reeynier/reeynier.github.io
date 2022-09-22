---
layout: post
title: "Diagonal Traverse Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Matrix, Simulation ]
similar: [ Matrix ]
featured: false
hidden: false
excerpt: LeetCode 498. Given an m x n matrix mat, return an array of all the elements of the array in a diagonal order.
---

<br />

## Description

LeetCode Problem 498.

Given an m x n matrix mat, return an array of all the elements of the array in a diagonal order.

Example 1: 
```
Input: mat = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,4,7,5,3,6,8,9]
```

Example 2:
```
Input: mat = [[1,2],[3,4]]
Output: [1,2,3,4]
```

Constraints:
* m == mat.length
* n == mat[i].length
* 1 <= m, n <= 10^4
* 1 <= m * n <= 10^4
* -10^5 <= mat[i][j] <= 10^5

<br />

## Sample C++ Code

The index sum (say it is i) of each round is from 0 to n+m-1. If the column index is j, then the row index is i-j. We need to ensure that j is in [0, m-1], and i-j is in [0, n-1]. Then j's value is between min(i, m-1) and max(i-n+1, 0).

```c
class Solution {
public:
    vector<int> findDiagonalOrder(vector<vector<int>>& matrix) {
        if (matrix.empty())
            return {};
        vector<int>res;
        int n = matrix.size(), m = matrix[0].size();
        for (int i = 0; i < n + m - 1; i++) { 
            if (i & 1) {
                for (int j = min(i, m - 1); j >= max(i - n + 1, 0); j--)
                    res.push_back(matrix[i - j][j]);
            } else {
                for (int j = max(i - n + 1, 0); j <= min(i, m - 1); j++)
                    res.push_back(matrix[i - j][j]);
            }
        }
        return res;
    }
};
```


