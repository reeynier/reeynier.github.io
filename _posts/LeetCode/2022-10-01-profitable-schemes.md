---
layout: post
title: "Profitable Schemes Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 879. There is a group of n members, and a list of various crimes they could commit. The i^th crime generates a profit[i] and requires group[i] members to participate in it. If a member participates in one crime, that member can't participate in another crime.

---

<br />

## Description

LeetCode Problem 879.

There is a group of n members, and a list of various crimes they could commit. The i^th crime generates a profit[i] and requires group[i] members to participate in it. If a member participates in one crime, that member can't participate in another crime.

Let's call a profitable scheme any subset of these crimes that generates at least minProfit profit, and the total number of members participating in that subset of crimes is at most n.
Return the number of schemes that can be chosen. Since the answer may be very large, return it modulo 10^9 + 7.

Example 1:
```
Input: n = 5, minProfit = 3, group = [2,2], profit = [2,3]
Output: 2
Explanation: To make a profit of at least 3, the group could either commit crimes 0 and 1, or just crime 1.
In total, there are 2 schemes.
```

Example 2:
```
Input: n = 10, minProfit = 5, group = [2,3,5], profit = [6,7,8]
Output: 7
Explanation: To make a profit of at least 5, the group could commit any crimes, as long as they commit one.
There are 7 possible schemes: (0), (1), (2), (0,1), (0,2), (1,2), and (0,1,2).
```

Constraints:
* 1 <= n <= 100
* 0 <= minProfit <= 100
* 1 <= group.length <= 100
* 1 <= group[i] <= 100
* profit.length == group.length
* 0 <= profit[i] <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    // dp[i][j] means the count of schemes with i profit and j members.
    // dp[i + p][j + g] += dp[i][j]) if i + p < P
    // dp[P][j + g] += dp[i][j]) if i + p >= P
    int profitableSchemes(int G, int P, vector<int> group, vector<int> profit) {
        vector<vector<int>> dp(P + 1, vector<int>(G + 1, 0));
        dp[0][0] = 1;
        int res = 0, mod = 1e9 + 7;
        for (int k = 0; k < group.size(); k++) {
            int g = group[k], p = profit[k];
            for (int i = P; i >= 0; i--)
                for (int j = G - g; j >= 0; j--)
                    dp[min(i + p, P)][j + g] = (dp[min(i + p, P)][j + g] + dp[i][j]) % mod;
        }
        for (int x: dp[P]) 
        	res = (res + x) % mod;
        return res;
    }
};
```


