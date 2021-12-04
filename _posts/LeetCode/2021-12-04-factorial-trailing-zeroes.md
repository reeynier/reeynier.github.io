---
layout: post
title: "Factorial Trailing Zeroes Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 172. Given an integer n, return the number of trailing zeroes in n!.

---

<br />

## Description

LeetCode Problem 172.

Given an integer n, return the number of trailing zeroes in n!.

Note that n! = n * (n - 1) * (n - 2) * ... * 3 * 2 * 1.

Example 1:
```
Input: n = 3
Output: 0
Explanation: 3! = 6, no trailing zero.
```

Example 2:
```
Input: n = 5
Output: 1
Explanation: 5! = 120, one trailing zero.
```

Example 3:
```
Input: n = 0
Output: 0
```

Constraints:
* 0 <= n <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int trailingZeroes(int n) {
        int zeros = 0;
        uint64_t p = 5;
        while (p <= n) {
            zeros += (n / p);
            p *= 5;
        }
        return zeros;
    }
};
```


