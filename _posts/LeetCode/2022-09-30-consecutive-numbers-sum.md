---
layout: post
title: "Consecutive Numbers Sum Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Enumeration ]
similar: [ Enumeration ]
featured: false
hidden: false
excerpt: LeetCode 829. Given an integer n, return the number of ways you can write n as the sum of consecutive positive integers.

---

<br />

## Description

LeetCode Problem 829.

Given an integer n, return the number of ways you can write n as the sum of consecutive positive integers.

Example 1:
```
Input: n = 5
Output: 2
Explanation: 5 = 2 + 3
```

Example 2:
```
Input: n = 9
Output: 3
Explanation: 9 = 4 + 5 = 2 + 3 + 4
```

Example 3:
```
Input: n = 15
Output: 4
Explanation: 15 = 8 + 7 = 4 + 5 + 6 = 1 + 2 + 3 + 4 + 5
```

Constraints:
* 1 <= n <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    int consecutiveNumbersSum(int n) {
        int cnt = 0, i = 1;
        while (n > 0) {
            n -= i;
            if (n % i == 0)
                cnt ++;
            i ++;
        }
        return cnt;
    }
};
```


