---
layout: post
title:  "Rotate Image Problem"
categories: [ Data Structure ]
tags: [ Array, Math, Leetcode ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 48. Determine if a 9 x 9 Sudoku board is valid.
---

<br />

## Description

LeetCode Problem 48. 

You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

 

Example 1:
```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [[7,4,1],[8,5,2],[9,6,3]]
```

Example 2:
```
Input: matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]
Output: [[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]
```

Example 3:
```
Input: matrix = [[1]]
Output: [[1]]
```

Example 4:
```
Input: matrix = [[1,2],[3,4]]
Output: [[3,1],[4,2]]
```

Constraints:

* matrix.length == n
* matrix[i].length == n
* 1 <= n <= 20
* -1000 <= matrix[i][j] <= 1000



<br />

## Sample C++ Code


```c
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        
        int b = 0, e = n;
        int tmp;
        while (b <= e) {
            for (int i = b; i < e-1; i ++) {
                tmp = matrix[b][i];
                matrix[b][i] = matrix[e-i+b-1][b];
                matrix[e-i+b-1][b] = matrix[e-1][e-i+b-1];
                matrix[e-1][e-i+b-1] = matrix[i][e-1];
                matrix[i][e-1] = tmp;
            }
            b ++, e --;
        }
    }
};
```
