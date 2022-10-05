---
layout: post
title: "Super Egg Drop Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Binary Search, Dynamic Programming ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 887. You are given k identical eggs and you have access to a building with n floors labeled from 1 to n.

---

<br />

## Description

LeetCode Problem 887.

You are given k identical eggs and you have access to a building with n floors labeled from 1 to n.

You know that there exists a floor f where 0 <= f <= n such that any egg dropped at a floor higher than f will break, and any egg dropped at or below floor f will not break.

Each move, you may take an unbroken egg and drop it from any floor x (where 1 <= x <= n). If the egg breaks, you can no longer use it. However, if the egg does not break, you may reuse it in future moves.

Return the minimum number of moves that you need to determine with certainty what the value of f is.

Example 1:
```
Input: k = 1, n = 2
Output: 2
Explanation: 
Drop the egg from floor 1. If it breaks, we know that f = 0.
Otherwise, drop the egg from floor 2. If it breaks, we know that f = 1.
If it does not break, then we know f = 2.
Hence, we need at minimum 2 moves to determine with certainty what the value of f is.
```

Example 2:
```
Input: k = 2, n = 6
Output: 3
```

Example 3:
```
Input: k = 3, n = 14
Output: 4
```

Constraints:
* 1 <= k <= 100
* 1 <= n <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    // dp[M][K]means that, given K eggs and M moves,
    // what is the maximum number of floor that we can check.
    // The dp equation is:
    // dp[m][k] = dp[m - 1][k - 1] + dp[m - 1][k] + 1,
    // which means we take 1 move to a floor,
    // if egg breaks, then we can check dp[m - 1][k - 1] floors.
    // if egg doesn't breaks, then we can check dp[m - 1][k] floors.
    // dp[m][k] is the number of combinations and it increase exponentially to N
    int superEggDrop(int K, int N) {
        vector<vector<int>> dp(N + 1, vector<int>(K + 1, 0));
        int m = 0;
        while (dp[m][K] < N) {
            m++;
            for (int k = 1; k <= K; ++k)
                dp[m][k] = dp[m - 1][k - 1] + dp[m - 1][k] + 1;
        }
        return m;
    }
};
```


