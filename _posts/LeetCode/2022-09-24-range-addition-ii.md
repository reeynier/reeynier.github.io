---
layout: post
title: "Range Addition II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math ]
similar: [ Array, Math ]
featured: false
hidden: false
excerpt: LeetCode 598. You are given an m x n matrix M initialized with all 0's and an array of operations ops, where ops[i] = [a_i, b_i] means M[x][y] should be incremented by one for all 0 <= x < a_i and 0 <= y < b_i.

---

<br />

## Description

LeetCode Problem 598.

You are given an m x n matrix M initialized with all 0's and an array of operations ops, where ops[i] = [a_i, b_i] means M[x][y] should be incremented by one for all 0 <= x < a_i and 0 <= y < b_i.
Count and return the number of maximum integers in the matrix after performing all the operations.

Example 1: 
```
Input: m = 3, n = 3, ops = [[2,2],[3,3]]
Output: 4
Explanation: The maximum integer in M is 2, and there are four of it in M. So return 4.
```

Example 2:
```
Input: m = 3, n = 3, ops = [[2,2],[3,3],[3,3],[3,3],[2,2],[3,3],[3,3],[3,3],[2,2],[3,3],[3,3],[3,3]]
Output: 4
```

Example 3:
```
Input: m = 3, n = 3, ops = []
Output: 9
```

Constraints:
* 1 <= m, n <= 4 * 10^4
* 0 <= ops.length <= 10^4
* ops[i].length == 2
* 1 <= a_i <= m
* 1 <= b_i <= n

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maxCount(int m, int n, vector<vector<int>>& ops) {
        int min_row = m;
        int min_col = n;
        for (int i = 0; i < ops.size(); i++) {
            if (ops[i][0] < min_row) min_row = ops[i][0];
            if (ops[i][1] < min_col) min_col = ops[i][1];
        }        
        return min_row*min_col;
    }
};
```


