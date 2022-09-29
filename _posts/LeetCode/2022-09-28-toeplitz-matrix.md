---
layout: post
title: "Toeplitz Matrix Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Matrix ]
similar: [ Matrix ]
featured: false
hidden: false
excerpt: LeetCode 766. Given an m x n matrix, returntrueif the matrix is Toeplitz. Otherwise, return false.

---

<br />

## Description

LeetCode Problem 766.

Given an m x n matrix, returntrueif the matrix is Toeplitz. Otherwise, return false.

A matrix is Toeplitz if every diagonal from top-left to bottom-right has the same elements.

Example 1: 
```
Input: matrix = [[1,2,3,4],[5,1,2,3],[9,5,1,2]]
Output: true
Explanation:
In the above grid, thediagonals are:
"[9]", "[5, 5]", "[1, 1, 1]", "[2, 2, 2]", "[3, 3]", "[4]".
In each diagonal all elements are the same, so the answer is True.
```

Example 2: 
```
Input: matrix = [[1,2],[2,2]]
Output: false
Explanation:
The diagonal "[1, 2]" has different elements.
```

Constraints:
* m == matrix.length
* n == matrix[i].length
* 1 <= m, n <= 20
* 0 <= matrix[i][j] <= 99

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isToeplitzMatrix(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        for (int i = 1; i < m; i++)
            for (int j = 1; j < n; j++)
                if (matrix[i][j] != matrix[i - 1][j - 1])
                    return false;
        return true;
    }
};
```


