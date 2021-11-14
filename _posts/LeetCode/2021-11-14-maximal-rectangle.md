---
layout: post
title:  "Maximal Rectangle Problem"
categories: [ Algorithm ]
tags: [ Array, Dynamic Programming, Stack, Leetcode ]
similar: [ Stack ]
featured: false
hidden: false
excerpt: LeetCode 85. Given a rows x cols binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.
---

<br />

## Description

LeetCode Problem 85. 

Given a rows x cols binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

 

Example 1:
```
Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 6
Explanation: The maximal rectangle is shown in the above picture.
```

Example 2:
```
Input: matrix = []
Output: 0
```

Example 3:
```
Input: matrix = [["0"]]
Output: 0
```

Example 4:
```
Input: matrix = [["1"]]
Output: 1
```

Example 5:
```
Input: matrix = [["0","0"]]
Output: 0
```

Constraints:

* rows == matrix.length
* cols == matrix[i].length
* 0 <= row, cols <= 200
* matrix[i][j] is '0' or '1'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maximalRectangle(vector<vector<char>>& matrix) {
        int r = matrix.size();
        if (r == 0) return 0;
        int c = matrix[0].size();
        
        int max_area = 0;
        int area, k, tp;
        stack<int> s;
        vector<int> line;
        vector<vector<int>> dp;
        
        for (int i = 0; i < r; i ++) {
            line.clear();
            for (int j = 0; j < c; j ++) {
                if (matrix[i][j] == '0')
                    line.push_back(0);
                else {
                    if (i > 0)
                        line.push_back(dp[i-1][j] + 1);
                    else 
                        line.push_back(matrix[i][j] - '0');
                }
            }   
            dp.push_back(line);
            
            k = 0;
            while (k < c) {
                if ((s.empty()) || (line[s.top()] < line[k])) {
                    s.push(k);
                    k ++;
                } else {
                    tp = s.top();
                    s.pop();
                    area = line[tp] * (s.empty() ? k : k - s.top() - 1);
                    if (area > max_area)
                        max_area = area;
                }
            }
            while (!s.empty()) {
                tp = s.top();
                s.pop();
                area = line[tp] * (s.empty() ? k : k - s.top() - 1);
                if (area > max_area)
                    max_area = area;
            }
        }
        return max_area;
    }
};
```
