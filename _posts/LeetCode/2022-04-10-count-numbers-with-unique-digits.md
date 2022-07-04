---
layout: post
title: "Count Numbers With Unique Digits Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Dynamic Programming, Backtracking ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 357. Given an integer n, return the count of all numbers with unique digits, x, where 0 <= x < 10^n.

---

<br />

## Description

LeetCode Problem 357.

Given an integer n, return the count of all numbers with unique digits, x, where 0 <= x < 10^n.

Example 1:
```
Input: n = 2
Output: 91
Explanation: The answer should be the total numbers in the range of 0 &le; x < 100, excluding 11,22,33,44,55,66,77,88,99
```

Example 2:
```
Input: n = 0
Output: 1
```

Constraints:
* 0 <= n <= 8

<br />

## Sample C++ Code


```c
/*
For n = 0, ans = 1
For n = 1, ans = 10
If we take 2 digit number, we have 9 options for first digit (1 - 9)
and 9 options for second digit(0 & all other digits except the one taken as first digit (to keep digits unique)) therefore ans += (9 * 9)
Similarly if we take 3 digit number we have 8 options for third digit, therefore ans += (9 * 9 * 8)
*/
class Solution {
public:
    int countNumbersWithUniqueDigits(int n) {
        if(n == 0)
            return 1;
        int ans = 10, calc = 9, temp = 9;
        for(int i = 0; i < n - 1; i++) {
            calc *= temp;
            ans += calc;
            temp--;
        }
        return ans;
    }
};
```


