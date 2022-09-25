---
layout: post
title: "Reshape The Matrix Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Matrix, Simulation ]
similar: [ Matrix ]
featured: false
hidden: false
excerpt: LeetCode 566. In MATLAB, there is a handy function called reshape which can reshape an m x n matrix into a new one with a different size r x c keeping its original data.

---

<br />

## Description

LeetCode Problem 566.

In MATLAB, there is a handy function called reshape which can reshape an m x n matrix into a new one with a different size r x c keeping its original data.

You are given an m x n matrix mat and two integers r and c representing the number of rows and the number of columns of the wanted reshaped matrix.

The reshaped matrix should be filled with all the elements of the original matrix in the same row-traversing order as they were.

If the reshape operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.

Example 1: 
```
Input: mat = [[1,2],[3,4]], r = 1, c = 4
Output: [[1,2,3,4]]
```

Example 2: 
```
Input: mat = [[1,2],[3,4]], r = 2, c = 4
Output: [[1,2],[3,4]]
```

Constraints:
* m == mat.length
* n == mat[i].length
* 1 <= m, n <= 100
* -1000 <= mat[i][j] <= 1000
* 1 <= r, c <= 300

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<vector<int>> matrixReshape(vector<vector<int>>& mat, int r, int c) {
        int m = size(mat), n = size(mat[0]), total = m * n;
        if (r * c != total) return mat;
        vector<vector<int>> ans(r, vector<int>(c));
        for (int i = 0; i < total; i++) 
            ans[i / c][i % c] = mat[i / n][i % n];
        return ans;
    }
};
```


