---
layout: post
title: "Binary Number With Alternating Bits Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Bit Manipulation ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 693. Given a positive integer, check whether it has alternating bits, namely, if two adjacent bits will always have different values.

---

<br />

## Description

LeetCode Problem 693.

Given a positive integer, check whether it has alternating bits: namely, if two adjacent bits will always have different values.

Example 1:
```
Input: n = 5
Output: true
Explanation: The binary representation of 5 is: 101
```

Example 2:
```
Input: n = 7
Output: false
Explanation: The binary representation of 7 is: 111.
```

Example 3:
```
Input: n = 11
Output: false
Explanation: The binary representation of 11 is: 1011.
```

Example 4:
```
Input: n = 10
Output: true
Explanation: The binary representation of 10 is: 1010.
```

Example 5:
```
Input: n = 3
Output: false
```

Constraints:
* 1 <= n <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool hasAlternatingBits(int n) {
        int d = n & 1;
        while ((n & 1) == d) {
            d = 1 - d;
            n >>= 1;
        }
        return n == 0;
    }
};
```


