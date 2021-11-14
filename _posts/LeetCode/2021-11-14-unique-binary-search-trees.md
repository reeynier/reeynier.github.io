---
layout: post
title:  "Unique Binary Search Trees Problem"
categories: [ Algorithm ]
tags: [ Math, Dynamic Programming, Tree, Binary Search Tree, Binary Tree, Leetcode ]
similar: [ Binary Search Tree ]
featured: false
hidden: false
excerpt: LeetCode 96. Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.
---

<br />

## Description

LeetCode Problem 96. 

Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.

 

Example 1:
```
Input: n = 3
Output: 5
```

Example 2:
```
Input: n = 1
Output: 1
```

Constraints:

* 1 <= n <= 19

<br />

## Sample C++ Code


```c
class Solution {
public:
    int numTrees(int n) {
        if(n <= 1) return 1;
        int ans = 0;
        for(int i = 1; i <= n; i++) 
            ans += numTrees(i-1) * numTrees(n-i);
        return ans;
    }
};
```
