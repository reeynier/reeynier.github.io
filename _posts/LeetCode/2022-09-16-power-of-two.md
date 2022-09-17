---
layout: post
title: "Power Of Two Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Bit Manipulation, Recursion ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 231. Given an integer n, return true if it is a power of two. Otherwise, return false.

---

<br />

## Description

LeetCode Problem 231.

Given an integer n, return true if it is a power of two. Otherwise, return false.

An integer n is a power of two, if there exists an integer x such that n == 2^x.

Example 1:
```
Input: n = 1
Output: true
Explanation: 2^0 = 1
```

Example 2:
```
Input: n = 16
Output: true
Explanation: 2^4 = 16
```

Example 3:
```
Input: n = 3
Output: false
```

Example 4:
```
Input: n = 4
Output: true
```

Example 5:
```
Input: n = 5
Output: false
```

Constraints:
* -2^31 <= n <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isPowerOfTwo(int n) {
        if (n <= 0)
            return false;
        while (n > 1) {
            if (n & 1 == 1)
                return false;
            n = n >> 1;
        }
        return true;
    }
};
```


