---
layout: post
title: "Sum Of Square Numbers Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Two Pointers, Binary Search ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 633. Given a non-negative integer c, decide whether there're two integers a and b such that a^2 + b^2 = c.

---

<br />

## Description

LeetCode Problem 633.

Given a non-negative integer c, decide whether there're two integers a and b such that a^2 + b^2 = c.

Example 1:
```
Input: c = 5
Output: true
Explanation: 1 * 1 + 2 * 2 = 5
```

Example 2:
```
Input: c = 3
Output: false
```

Example 3:
```
Input: c = 4
Output: true
```

Example 4:
```
Input: c = 2
Output: true
```

Example 5:
```
Input: c = 1
Output: true
```

Constraints:
* 0 <= c <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool judgeSquareSum(int c) {
        if (c < 0)
            return false;
        long int left = 0, right = sqrt(c);
        while (left <= right) {
            long int cur = left * left + right * right;
            if (cur < c)
                left ++;
            else if (cur > c)
                right --;
            else 
                return true;
        }
        return false;
    }
};
```


