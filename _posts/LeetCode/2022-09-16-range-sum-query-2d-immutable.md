---
layout: post
title: "Range Sum Query 2D - Immutable Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Design, Matrix, Prefix Sum ]
similar: [ Design ]
featured: false
hidden: false
excerpt: LeetCode 304. Given a 2D matrix matrix, handle multiple queries of the following type

---

<br />

## Description

LeetCode Problem 304.

Given a 2D matrix matrix, handle multiple queries of the following type:
* Calculate the sum of the elements of matrix inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).
Implement the NumMatrix class:
* NumMatrix(int[][] matrix) Initializes the object with the integer matrix matrix.
* int sumRegion(int row1, int col1, int row2, int col2) Returns the sum of the elements of matrix inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).

Example 1:
```
Input
["NumMatrix", "sumRegion", "sumRegion", "sumRegion"]
[[[[3, 0, 1, 4, 2], [5, 6, 3, 2, 1], [1, 2, 0, 1, 5], [4, 1, 0, 1, 7], [1, 0, 3, 0, 5]]], [2, 1, 4, 3], [1, 1, 2, 2], [1, 2, 2, 4]]
Output
[null, 8, 11, 12]
Explanation
NumMatrix numMatrix = new NumMatrix([[3, 0, 1, 4, 2], [5, 6, 3, 2, 1], [1, 2, 0, 1, 5], [4, 1, 0, 1, 7], [1, 0, 3, 0, 5]]);
numMatrix.sumRegion(2, 1, 4, 3); // return 8 (i.e sum of the red rectangle)
numMatrix.sumRegion(1, 1, 2, 2); // return 11 (i.e sum of the green rectangle)
numMatrix.sumRegion(1, 2, 2, 4); // return 12 (i.e sum of the blue rectangle)
```

Constraints:
* m == matrix.length
* n == matrix[i].length
* 1 <= m, n <= 200
* -10^5 <= matrix[i][j] <= 10^5
* 0 <= row1 <= row2 < m
* 0 <= col1 <= col2 < n
* At most 10^4 calls will be made to sumRegion.

<br />

## Sample C++ Code


```c
class NumMatrix {
public:
    vector<vector<int>> dp;
    int m = 0, n = 0;
    
    NumMatrix(vector<vector<int>>& matrix) {
        m = matrix.size();
        if (m == 0) return;    
        n = matrix[0].size();
        
        vector<int> linesum(n, 0);
        vector<vector<int>> vecsum(m, vector<int>(n, 0));
        for (int i = 0; i < m; i ++) {
            linesum.clear();
            for (int j = 0; j < n; j ++) {
                if (j == 0) {
                    linesum[j] = matrix[i][j];
                } else {
                    linesum[j] = linesum[j-1] + matrix[i][j];
                }
                if (i == 0) {
                    vecsum[i][j] = linesum[j];
                } else {
                    vecsum[i][j] = linesum[j] + vecsum[i-1][j];
                }
            }
        }
        dp = vecsum;
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        if (m == 0 || n == 0)
            return 0;
        int ans = dp[row2][col2];
        if (row1 >= 1) {
            ans -= dp[row1-1][col2];
        }
        if (col1 >= 1) {
            ans -= dp[row2][col1-1];
        }
        if (row1 >= 1 && col1 >= 1) {
            ans += dp[row1-1][col1-1];
        }
        return ans;
    }
};

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix* obj = new NumMatrix(matrix);
 * int param_1 = obj->sumRegion(row1,col1,row2,col2);
 */
```


