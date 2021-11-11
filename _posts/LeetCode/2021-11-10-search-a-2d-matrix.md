---
layout: post
title:  "Search A 2D Matrix Problem"
categories: [ Algorithm ]
tags: [ Array, Binary Search, Leetcode ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 74. Write an efficient algorithm that searches for a value in an m x n matrix. 
---

<br />

## Description

LeetCode Problem 74. 

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.
 

Example 1:
```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```

Example 2:
```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
```
 

Constraints:

* m == matrix.length
* n == matrix[i].length
* 1 <= m, n <= 100
* -10^4 <= matrix[i][j], target <= 10^4



<br />

## Sample C++ Code


```c
class Solution {
public:
    bool searchMatrix(vector<vector<int> > &matrix, int target) {
        // Use binary search.
        // n * m matrix convert to an array => matrix[x][y] => a[x * m + y]
        // an array convert to n * m matrix => a[x] =>matrix[x / m][x % m];
        int n = matrix.size();
        int m = matrix[0].size();
        int l = 0, r = m * n - 1;
        while (l != r){
            int mid = (l + r - 1) >> 1;
            if (matrix[mid / m][mid % m] < target)
                l = mid + 1;
            else 
                r = mid;
        }
        return matrix[r / m][r % m] == target;
    }
};
```
