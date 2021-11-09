---
layout: post
title:  "N-Queens II Problem"
categories: [ Algorithm ]
tags: [ Array, Backtracking, Leetcode ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 52. Given an integer n, return the number of distinct solutions to the n-queens puzzle.
---

<br />

## Description

LeetCode Problem 52. 

The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.

Given an integer n, return the number of distinct solutions to the n-queens puzzle.

 

Example 1:
```
Input: n = 4
Output: 2
Explanation: There are two distinct solutions to the 4-queens puzzle as shown.
```

Example 2:
```
Input: n = 1
Output: 1
```
 

Constraints:

* 1 <= n <= 9


<br />

## Sample C++ Code


```c
class Solution {
public:
    int cnt;
    int N;
    
    void dfs(vector<int>& col2row, int row) {
        if (row == N) {
            cnt ++;
            return;
        }
        
        int r, c;
        bool place;
        vector<vector<int>> dir = { {-1,-1}, {1,1}, {-1,1}, {1,-1} };
        for (int col = 0; col < N; col ++) {
            if (col2row[col] == -1) {
                place = true;
                for (int j = 0; j < 4; j ++) {
                    r = row + dir[j][0], c = col + dir[j][1];
                    while (r >= 0 && r < N && c >= 0 && c < N && place) {
                        if (col2row[c] == r) {
                            place = false;
                            break;
                        }
                        r += dir[j][0], c += dir[j][1];
                    }
                    if (!place)
                        break;
                }
                if (place) {
                    col2row[col] = row;
                    dfs(col2row, row+1);
                    col2row[col] = -1;
                }
            }
        }
    }
    
    int totalNQueens(int n) {
        cnt = 0, N = n;
        vector<int> col2row(n, -1);
        dfs(col2row, 0);
        return cnt;
    }
};
```
