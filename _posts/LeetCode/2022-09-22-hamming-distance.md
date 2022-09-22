---
layout: post
title: "Hamming Distance Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Bit Manipulation ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 461. The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

---

<br />

## Description

LeetCode Problem 461.

The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, return the Hamming distance between them.

Example 1:
```
Input: x = 1, y = 4
Output: 2
Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
&uarr;   &uarr;
The above arrows point to positions where the corresponding bits are different.
```

Example 2:
```
Input: x = 3, y = 1
Output: 1
```

Constraints:
* 0 <=x, y <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    int hammingDistance(int x, int y) {
        x = x ^ y;
        int dis = 0;
        while (x != 0) {
            dis += (x & 1);
            x = x >> 1;
        }
        return dis;
    }
};
```


