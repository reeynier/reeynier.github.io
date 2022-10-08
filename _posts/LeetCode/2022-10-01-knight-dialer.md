---
layout: post
title: "Knight Dialer Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 935. The chess knight has a unique movement, it may move two squares vertically and one square horizontally, or two squares horizontally and one square vertically (with both forming the shape of an L). The possible movements of chess knight are shown in this diagaram

---

<br />

## Description

LeetCode Problem 935.

The chess knight has a unique movement, it may move two squares vertically and one square horizontally, or two squares horizontally and one square vertically (with both forming the shape of an L). 

Given an integer n, return how many distinct phone numbers of length n we can dial.

You are allowed to place the knight on any numeric cell initially and then you should perform n - 1 jumps to dial a number of length n. All jumps should be valid knight jumps.

As the answer may be very large, return the answer modulo 10^9 + 7.

Example 1:
```
Input: n = 1
Output: 10
Explanation: We need to dial a number of length 1, so placing the knight over any numeric cell of the 10 cells is sufficient.
```

Example 2:
```
Input: n = 2
Output: 20
Explanation: All the valid number we can dial are [04, 06, 16, 18, 27, 29, 34, 38, 40, 43, 49, 60, 61, 67, 72, 76, 81, 83, 92, 94]
```

Example 3:
```
Input: n = 3
Output: 46
```

Example 4:
```
Input: n = 4
Output: 104
```

Example 5:
```
Input: n = 3131
Output: 136006598
Explanation: Please take care of the mod.
```

Constraints:
* 1 <= n <= 5000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int knightDialer(int n) {
        vector<vector<int>> moves = { {4,6}, {6,8}, {7,9}, {4,8}, 
                               {0,3,9}, {}, {0,1,7}, {2,6}, {1,3}, {2,4} };
        
        int m = pow(10, 9)+7;
        if (n == 0) return 0;
        if (n == 1) return 10;
        
        vector<vector<uint64_t>> dp(10, vector<uint64_t>(n+1, 0));
        for (int i = 0; i < 10; i ++)
            dp[i][0] = 1;
        
        for (int i = 1; i < n; i ++) {
            for (int j = 0; j < 10; j ++) {
                for (int k = 0; k < moves[j].size(); k ++) {
                    dp[j][i] += dp[moves[j][k]][i-1];
                    dp[j][i] %= m;
                }
            }
        }
        
        uint64_t sum = 0;
        for (int i = 0; i < 10; i ++) {
            sum += dp[i][n-1];
            sum %= m;
        }
        
        return sum;
    }
};
```


