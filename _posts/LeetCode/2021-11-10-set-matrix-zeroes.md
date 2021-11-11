---
layout: post
title:  "Set Matrix Zeroes Problem"
categories: [ Data Structure ]
tags: [ Array, Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 73. Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's, and return the matrix.
---

<br />

## Description

LeetCode Problem 73. 

Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's, and return the matrix.

You must do it in place.

 

Example 1:
```
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```

Example 2:
```
Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
``` 

Constraints:

* m == matrix.length
* n == matrix[0].length
* 1 <= m, n <= 200
* -2^31 <= matrix[i][j] <= 2^31 - 1


<br />

## Sample C++ Code


```c
void setZeroes(vector<vector<int> > &matrix) {
    // Store states of each row in the first of that row, and store states of each column in the first of that column. 
    int col0 = 1, rows = matrix.size(), cols = matrix[0].size();

    for (int i = 0; i < rows; i++) {
        if (matrix[i][0] == 0) col0 = 0;
        for (int j = 1; j < cols; j++)
            if (matrix[i][j] == 0)
                matrix[i][0] = matrix[0][j] = 0;
    }

    for (int i = rows - 1; i >= 0; i--) {
        for (int j = cols - 1; j >= 1; j--)
            if (matrix[i][0] == 0 || matrix[0][j] == 0)
                matrix[i][j] = 0;
        if (col0 == 0) matrix[i][0] = 0;
    }
}
```
