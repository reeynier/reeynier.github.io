---
layout: post
title: "Domino And Tromino Tiling Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 790. You have two types of tiles, a 2 x 1 domino shape and a tromino shape. You may rotate these shapes.

---

<br />

## Description

LeetCode Problem 790.

You have two types of tiles: a 2 x 1 domino shape and a tromino shape. You may rotate these shapes.

Given an integer n, return the number of ways to tile an 2 x n board. Since the answer may be very large, return it modulo 10^9 + 7.

In a tiling, every square must be covered by a tile. Two tilings are different if and only if there are two 4-directionally adjacent cells on the board such that exactly one of the tilings has both squares occupied by a tile.

Example 1: 
```
Input: n = 3
Output: 5
Explanation: The five different ways are show above.
```

Example 2:
```
Input: n = 1
Output: 1
```

Constraints:
* 1 <= n <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
     /* Using 1-indexed Levels:
        dp1[i] denotes the number of ways with all cols from 1 to i filled
        dp2[i] denotes the number of ways with all cols from 1 to i - 1 filled and only top grid in col i is filled
        dp3[i] denotes the number of ways with all cols from 1 to i - 1 filled and only bottom grid in col i is filled

        Base Cases:
        dp1[1] = 1; dp1[2] = 2
        dp2[1] = 0; dp2[2] = 1
        dp3[1] = 0; dp3[2] = 1;

        DP relation: (for all i >= 3)
        dp1[i] = dp1[i - 1] (add 1 vertical domino) + dp1[i - 2] (add 2-horizontal dominoes)  + dp2[i - 1] (add 1 tromino in _| manner) + dp3[i - 1] (add 1 tromino such that top space in i - 1 col and i col gets filled)
        dp2[i] = dp1[i - 2] (put one tribonaaci) + dp3[i - 1] (put on domino in horizontal fashion)
        similarly => dp3[i] = dp1[i - 2] + dp2[i - 1]
    */
    int numTilings(int n) {
        if (n == 1)
            return 1;
        
        long long mod = 1e9+7;
     
        vector<long long int> dp1(n + 1, 0);
        vector<long long int> dp2(n + 1, 0);
        vector<long long int> dp3(n + 1, 0);
        
        dp1[1] = 1;
        dp1[2] = 2;
        dp2[1] = 0;
        dp2[2] = 1;
        dp3[1] = 0;
        dp3[2] = 1;
        
        for (int i = 3 ; i <= n ; i++) {
            dp1[i] = (dp1[i - 1] + dp1[i - 2] + dp2[i - 1]+ dp3[i - 1]) % mod;
            dp2[i] = (dp1[i - 2] + dp3[i - 1]) % mod;
            dp3[i] = (dp1[i - 2] + dp2[i - 1]) % mod;
        }
        
        return dp1[n];
    }
};
```


