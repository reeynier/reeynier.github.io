---
layout: post
title:  "Reverse Integer Problem"
categories: [ Algorithm ]
tags: [ Math, Leetcode ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 7. Given a signed 32-bit integer x, return x with its digits reversed.
---

<br />

## Description

LeetCode Problem 7. 

Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-2^31, 2^31 - 1], then return 0.

Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

 

Example 1:
```
Input: x = 123
Output: 321
```

Example 2:
```
Input: x = -123
Output: -321
```

Example 3:
```
Input: x = 120
Output: 21
```

Example 4:
```
Input: x = 0
Output: 0
```

Constraints:

* -2^31 <= x <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    int reverse(int x) {
        long long res = 0;
        while(x) {
            res = res*10 + x%10;
            x /= 10;
        }
        return (res<INT_MIN || res>INT_MAX) ? 0 : res;
    }
};
```
