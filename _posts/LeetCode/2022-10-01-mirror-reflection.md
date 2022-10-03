---
layout: post
title: "Mirror Reflection Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Geometry ]
similar: [ Geometry ]
featured: false
hidden: false
excerpt: LeetCode 858. There is a special square room with mirrors on each of the four walls. Except for the southwest corner, there are receptors on each of the remaining corners, numbered 0, 1, and 2.

---

<br />

## Description

LeetCode Problem 858.

There is a special square room with mirrors on each of the four walls. Except for the southwest corner, there are receptors on each of the remaining corners, numbered 0, 1, and 2.

The square room has walls of length pand a laser ray from the southwest corner first meets the east wall at a distance q from the 0^th receptor.

Given the two integers p and q, return the number of the receptor that the ray meets first.
The test cases are guaranteed so that the ray will meet a receptor eventually.

Example 1: 
```
Input: p = 2, q = 1
Output: 2
Explanation: The ray meets receptor 2 the first time it gets reflected back to the left wall.
```

Example 2:
```
Input: p = 3, q = 1
Output: 1
```

Constraints:
* 1 <= q <= p <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int gcd(int a, int b) {
        while (b) {
            a = a % b;
            swap(a, b);
        }
        return a;
    }
    
    int mirrorReflection (int p, int q) {
        int m = q / gcd(p, q);
        int n = p / gcd(p, q);
        if (m % 2 == 0 && n % 2 == 1) 
            return 0;
        if (m % 2 == 1 && n % 2 == 1) 
            return 1;
        if (m % 2 == 1 && n % 2 == 0) 
            return 2;
        return -1;
    }
};
```


