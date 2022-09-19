---
layout: post
title: "Search A 2D Matrix II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search, Divide and Conquer, Matrix ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 240. Write an efficient algorithm that searches for a target value in an m x n integer matrix. The matrix has the following properties

---

<br />

## Description

LeetCode Problem 240.

Write an efficient algorithm that searches for a target value in an m x n integer matrix. The matrix has the following properties:
* Integers in each row are sorted in ascending from left to right.
* Integers in each column are sorted in ascending from top to bottom.

Example 1:
```
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
Output: true
```

Example 2:
```
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20
Output: false
```

Constraints:
* m == matrix.length
* n == matrix[i].length
* 1 <= n, m <= 300
* -10^9 <= matrix[i][j] <= 10^9
* All the integers in each row are sorted in ascending order.
* All the integers in each column are sorted in ascending order.
* -10^9 <= target <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int row = matrix.size();
        if (row == 0) return false;
        int col = matrix[0].size();
        if (col == 0) return false;
        
        int l, r, m, pos;
        
        for (int i = 0; i < row; i ++) {
            l = 0, r = col-1;
            while (l <= r) {
                m = (l + r) / 2;
                if (matrix[i][m] == target)
                    return true;
                if (matrix[i][m] < target)
                    l = m + 1;
                else
                    r = m - 1;
                pos = m;
            }
            if (matrix[i][pos] == target)
                return true;
        }
        return false;
    }
};
```


