---
layout: post
title: "2 Keys Keyboard Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 650. There is only one character 'A' on the screen of a notepad. You can perform two operations on this notepad for each step

---

<br />

## Description

LeetCode Problem 650.

There is only one character 'A' on the screen of a notepad. You can perform two operations on this notepad for each step:
* Copy All: You can copy all the characters present on the screen (a partial copy is not allowed).
* Paste: You can paste the characters which are copied last time.

Given an integer n, return the minimum number of operations to get the character 'A' exactly n times on the screen.

Example 1:
```
Input: n = 3
Output: 3
Explanation: Intitally, we have one character 'A'.
In step 1, we use Copy All operation.
In step 2, we use Paste operation to get 'AA'.
In step 3, we use Paste operation to get 'AAA'.
```

Example 2:
```
Input: n = 1
Output: 0
```

Constraints:
* 1 <= n <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int helper(int i, int n, int copied) {
        if (i == n) {
            return 1;
        }
        if (i > n) {
            return INT_MAX / 2;
        }
        return min(2 + helper(2 * i, n, i), 1 + helper(i + copied, n, copied));
    }
    
    int minSteps(int n) {
       if (n == 1) {
           return 0;
       } 
        return helper(1, n, 1);
    }
};
```


