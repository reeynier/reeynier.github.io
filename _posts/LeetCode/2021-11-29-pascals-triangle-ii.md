---
layout: post
title: "Pascal's Triangle II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: []
featured: false
hidden: false
excerpt: LeetCode 119. Given an integer rowIndex, return the rowIndex^th (0-indexed) row of the Pascal's triangle.

---

<br />

## Description

LeetCode Problem 119.

Given an integer rowIndex, return the rowIndex^th (0-indexed) row of the Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it. 

Example 1:
```
Input: rowIndex = 3
Output: [1,3,3,1]
```

Example 2:
```
Input: rowIndex = 0
Output: [1]
```

Example 3:
```
Input: rowIndex = 1
Output: [1,1]
```

Constraints:
* 0 <= rowIndex <= 33

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector<int> A(rowIndex+1, 0);
        A[0] = 1;
        for(int i=1; i<rowIndex+1; i++)
            for(int j=i; j>=1; j--)
                A[j] += A[j-1];
        return A;
    }
};
```


