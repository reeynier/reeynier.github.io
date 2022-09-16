---
layout: post
title: "Number Of Digit One Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Dynamic Programming, Recursion ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 233. Given an integer n, count the total number of digit 1 appearing in all non-negative integers less than or equal to n.

---

<br />

## Description

LeetCode Problem 233.

Given an integer n, count the total number of digit 1 appearing in all non-negative integers less than or equal to n.

Example 1:
```
Input: n = 13
Output: 6
```

Example 2:
```
Input: n = 0
Output: 0
```

Constraints:
* 0 <= n <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    // Basic idea: count number of combination of 1 at each digit in two cases: prefix appears or not
    // Eg.3101592:
    // 1) one at hundreds:      1 (< 5): [1~3101]1[0~99]. So # = 3101 * 100 + 100 (Safe since 31011XX never be greater than 31015XX)
    // 2) one at thousands:     1 (= 1): [1~310]1[0~592]. So # = 310 * 1000 + (592 + 1) (Unsafe if prefix is 0, it must be <= 1592)
    // 3) one at ten thousands: 1 (> 0): [1~30]1[0~9999]. So # = 30 * 10000 (If prefix is 0, no 1 digit number exist)
    int countDigitOne(int n) {
    int ones = 0;
    for (long long m = 1; m <= n; m *= 10) {
        int a = n / m, b = n % m;
        ones += (a + 8) / 10 * m + (a % 10 == 1) * (b + 1);
    }
    return ones;
}
};
```


