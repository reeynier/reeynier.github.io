---
layout: post
title: "Fibonacci Number Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Dynamic Programming, Recursion, Memoization ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 509. The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. 

---

<br />

## Description

LeetCode Problem 509.

The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,

```
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.
```

Given n, calculate F(n).

Example 1:
```
Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
```

Example 2:
```
Input: n = 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
```

Example 3:
```
Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```

Constraints:
* 0 <= n <= 30

<br />

## Sample C++ Code


```c
class Solution {
public:
    int fib(int N) {
        if (N == 0)
            return 0;
        if (N == 1)
            return 1;
        return fib(N-1) + fib(N-2);
    }
};
```

```c
class Solution {
public:
    int fib(int N) {
        int dp[2] = {0, 1};

        for (int i = 2; i <= N; i++)
           dp[i % 2] = dp[0] + dp[1];

        return dp[N % 2];
    }
};
```
