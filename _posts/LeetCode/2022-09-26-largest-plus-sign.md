---
layout: post
title: "Largest Plus Sign Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 764. You are given an integer n. You have an n x n binary grid grid with all values initially 1's except for some indices given in the array mines. The i^th element of the array mines is defined as mines[i] = [x_i, y_i] where grid[x_i][y_i] == 0.

---

<br />

## Description

LeetCode Problem 764.

You are given an integer n. You have an n x n binary grid grid with all values initially 1's except for some indices given in the array mines. The i^th element of the array mines is defined as mines[i] = [x_i, y_i] where grid[x_i][y_i] == 0.

Return the order of the largest axis-aligned plus sign of 1's contained in grid. If there is none, return 0.

An axis-aligned plus sign of 1's of order k has some center grid[r][c] == 1 along with four arms of length k - 1 going up, down, left, and right, and made of 1's. Note that there could be 0's or 1's beyond the arms of the plus sign, only the relevant area of the plus sign is checked for 1's.

Example 1: 
```
Input: n = 5, mines = [[4,2]]
Output: 2
Explanation: In the above grid, the largest plus sign can only be of order 2. One of them is shown.
```

Example 2: 
```
Input: n = 1, mines = [[0,0]]
Output: 0
Explanation: There is no plus sign, so return 0.
```

Constraints:
* 1 <= n <= 500
* 1 <= mines.length <= 5000
* 0 <= x_i, y_i < n
* All the pairs (x_i, y_i) are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int orderOfLargestPlusSign(int n, vector<vector<int>>& mines) {
        int u[n][n], d[n][n], l[n][n], r[n][n];
        vector<vector<int>> grid(n, vector<int>(n, 1));

        for (auto &e : mines) {
            grid[e[0]][e[1]] = 0;
        }

        for (int i = 0; i < n; ++i) {
            int sum = 0;
            for (int j = 0; j < n; ++j) {
                if (!grid[i][j]) sum = 0;
                else {
                    sum += grid[i][j];
                }
                l[i][j] = sum;
            }
        }

        for (int i = 0; i < n; ++i) {
            int sum = 0;
            for (int j = n - 1; j >= 0; --j) {
                if (!grid[i][j]) sum = 0;
                else {
                    sum += grid[i][j];
                }
                r[i][j] = sum;
            }
        }

        for (int i = 0; i < n; ++i) {
            int sum = 0;
            for (int j = 0; j < n; ++j) {
                if (!grid[j][i]) sum = 0;
                else {
                    sum += grid[j][i];
                }
                u[j][i] = sum;
            }
        }

        for (int i = 0; i < n; ++i) {
            int sum = 0;
            for (int j = n - 1; j >= 0; --j) {
                if (!grid[j][i]) sum = 0;
                else {
                    sum += grid[j][i];
                }
                d[j][i] = sum;
            }
        }

        int ans = INT_MIN;
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n; ++j) {
                ans = max(ans, min(min(u[i][j], d[i][j]), min(l[i][j], r[i][j])));
            }
        }
        return ans;
    }
};
```


