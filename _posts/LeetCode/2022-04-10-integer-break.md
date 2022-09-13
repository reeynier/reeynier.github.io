---
layout: post
title: "Integer Break Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 343. Given an integer n, break it into the sum of k positive integers, where k >= 2, and maximize the product of those integers.

---

<br />

## Description

LeetCode Problem 343.

Given an integer n, break it into the sum of k positive integers, where k >= 2, and maximize the product of those integers.

Return the maximum product you can get.

Example 1:
```
Input: n = 2
Output: 1
Explanation: 2 = 1 + 1, 1 &times; 1 = 1.
```

Example 2:
```
Input: n = 10
Output: 36
Explanation: 10 = 3 + 3 + 4, 3 &times; 3 &times; 4 = 36.
```

Constraints:
* 2 <= n <= 58

<br />

## Sample C++ Code


```c
class Solution {
public:
    int integerBreak(int n) {
        vector<int> dp(n + 1, 0);
        for(int i = 2; i <= n; i++) {
            for(int j = 1; j <= i / 2; j++) {
                dp[i] = max(dp[i], max(j, dp[j]) * max(i - j, dp[i - j]));
            }
        }
        return dp[n];
    }
};
```


