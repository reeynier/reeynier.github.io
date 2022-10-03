---
layout: post
title: "Minimum Falling Path Sum Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Matrix ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 931. Given an n x n array of integers matrix, return the minimum sum of any falling path through matrix.

---

<br />

## Description

LeetCode Problem 931.

Given an n x n array of integers matrix, return the minimum sum of any falling path through matrix.

A falling path starts at any element in the first row and chooses the element in the next row that is either directly below or diagonally left/right. Specifically, the next element from position (row, col) will be (row + 1, col - 1), (row + 1, col), or (row + 1, col + 1).

Example 1: 
```
Input: matrix = [[2,1,3],[6,5,4],[7,8,9]]
Output: 13
Explanation: There are two falling paths with a minimum sum as shown.
```

Example 2: 
```
Input: matrix = [[-19,57],[-40,-5]]
Output: -59
Explanation: The falling path with a minimum sum is shown.
```

Constraints:
* n == matrix.length == matrix[i].length
* 1 <= n <= 100
* -100 <= matrix[i][j] <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    int minFallingPathSum(vector<vector<int>>& A) {
        if (A.size() == 0)
            return 0;
        int r = A.size(), c = A[0].size();
        vector<vector<int>> dp(r+1, vector<int>(c+2, 0));
        
        for (int i = 1; i <= r; i ++) {
            for (int j = 1; j <= c; j ++) {
                if (j == 1) {
                    dp[i][j] = min(dp[i-1][j], dp[i-1][j+1]) + A[i-1][j-1];
                } else if (j == c) {
                    dp[i][j] = min(dp[i-1][j-1], dp[i-1][j]) + A[i-1][j-1];
                } else {
                    dp[i][j] = min(dp[i-1][j-1], dp[i-1][j]);
                    dp[i][j] = min(dp[i][j], dp[i-1][j+1]);
                    dp[i][j] += A[i-1][j-1];
                }
            }
        }
        int min_sum = INT_MAX;
        for (int i = 1; i <= c; i ++) {
            if (dp[r][i] < min_sum) {
                min_sum = dp[r][i];
            }
        }
        return min_sum;
    }
};
```


