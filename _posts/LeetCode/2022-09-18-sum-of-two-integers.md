---
layout: post
title: "Sum Of Two Integers Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Bit Manipulation ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 371. Given two integers a and b, return the sum of the two integers without using the operators + and -.

---

<br />

## Description

LeetCode Problem 371.

Given two integers a and b, return the sum of the two integers without using the operators + and -.

Example 1:
```
Input: a = 1, b = 2
Output: 3
```

Example 2:
```
Input: a = 2, b = 3
Output: 5
```

Constraints:
* -1000 <= a, b <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int getSum(int a, int b) {
        int sum = 0, c = 0;
        int p, q, n = 1, s, i = 1;
        bool neg;
        if (a < 0 && b < 0)
            neg = true;
        else if ((a < 0 && -(unsigned int)a > b) || (b < 0 && -(unsigned int)b > a))
            neg = true;
        else
            neg = false;
        
        while (i < 32) {
            p = a & 1, q = b & 1;
            s = p ^ q ^ c;
            c = (p & q) || (p & c) || (q & c);
            sum = (s == 1) ? (sum | n) : (sum);
            n = n << 1, a = a >> 1, b = b >> 1;
            i ++;
        }
        
        if (neg && sum != 0)
            sum -= 2147483648;

        return sum;
    }
};
```


