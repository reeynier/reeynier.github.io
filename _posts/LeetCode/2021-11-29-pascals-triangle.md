---
layout: post
title: "Pascal's Triangle Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 118. Given an integer numRows, return the first numRows of Pascal's triangle.

---

<br />

## Description

LeetCode Problem 118.

Given an integer numRows, return the first numRows of Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it.

Example 1:
```
Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```

Example 2:
```
Input: numRows = 1
Output: [[1]]
```

Constraints:
* 1 <= numRows <= 30

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> ans(numRows, vector<int>());
        if (numRows == 0)
            return ans;
        ans[0].push_back(1);
        
        for (int i = 1; i < numRows; i ++) {
            ans[i].push_back(1);
            for (int j = 0; j < ans[i-1].size() - 1; j ++) {
                ans[i].push_back(ans[i-1][j] + ans[i-1][j+1]);        
            }
            ans[i].push_back(1);
        }
        
        return ans;
    }
};
```


