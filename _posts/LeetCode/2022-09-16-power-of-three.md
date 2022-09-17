---
layout: post
title: "Power Of Three Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Recursion ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 326. Given an integer n, return true if it is a power of three. Otherwise, return false.

---

<br />

## Description

LeetCode Problem 326.

Given an integer n, return true if it is a power of three. Otherwise, return false.

An integer n is a power of three, if there exists an integer x such that n == 3^x.

Example 1:
```
Input: n = 27
Output: true
```

Example 2:
```
Input: n = 0
Output: false
```

Example 3:
```
Input: n = 9
Output: true
```

Example 4:
```
Input: n = 45
Output: false
```

Constraints:
* -2^31 <= n <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isPowerOfThree(int n) {
        if (n == 1)
            return true;
        if (n <= 0 || n % 3 != 0)
            return false;
        return isPowerOfThree(double(n) / 3);
    }
};
```


