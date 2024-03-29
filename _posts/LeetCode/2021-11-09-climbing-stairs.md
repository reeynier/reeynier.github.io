---
layout: post
title:  "Climbing Stairs Problem"
categories: [ Data Structure ]
tags: [ Math, Dynamic Programming, Leetcode ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 70. You are climbing a staircase. It takes n steps to reach the top.
---

<br />

## Description

LeetCode Problem 70. 

You are climbing a staircase. It takes n steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

 

Example 1:
```
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

Example 2:
```
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

Constraints:

* 1 <= n <= 45

<br />

## Sample C++ Code


```c
class Solution {
public:
    int climbStairs(int n) {
        int f1 = 1;
        int f2 = 2;
        
        if (n == 1)
            return f1;
        if (n == 2)
            return f2;
        
        int f;
        for (int i = 3; i <= n; i ++) {
            f = f1 + f2;
            f1 = f2;
            f2 = f;
        }
        
        return f;
    }
};
```
