---
layout: post
title: "Maximal Square Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Matrix ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 221. Given an m x n binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

---

<br />

## Description

LeetCode Problem 221.

Given an m x n binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

Example 1:
```
Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 4
```

Example 2:
```
Input: matrix = [["0","1"],["1","0"]]
Output: 1
```

Example 3:
```
Input: matrix = [["0"]]
Output: 0
```

Constraints:
* m == matrix.length
* n == matrix[i].length
* 1 <= m, n <= 300
* matrix[i][j] is '0' or '1'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        int maxSquare = 0;
        int m = matrix.size();
        if (m == 0) return 0;
        int n = matrix[0].size();
        
        int l;
        int maxL = 0;
        vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
        for (int i = 1; i <= m; i ++) {
            for (int j = 1; j <= n; j ++) {
                if (matrix[i-1][j-1] == '1') {
                    l = min(dp[i-1][j], dp[i][j-1]);
                    if (matrix[i-l-1][j-l-1] == '1')
                        dp[i][j] = l + 1;
                    else
                        dp[i][j] = l;
                    maxL = max(maxL, dp[i][j]);
                }
                //cout << dp[i][j] << " ";
            }
            cout << endl;
        }
        return maxL*maxL;
    }
};
```


