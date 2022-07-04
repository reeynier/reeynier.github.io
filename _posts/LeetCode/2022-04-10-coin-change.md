---
layout: post
title: "Coin Change Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Breadth-First Search ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 322. You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

---

<br />

## Description

LeetCode Problem 322.

You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

Example 1:
```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```

Example 2:
```
Input: coins = [2], amount = 3
Output: -1
```

Example 3:
```
Input: coins = [1], amount = 0
Output: 0
```

Example 4:
```
Input: coins = [1], amount = 1
Output: 1
```

Example 5:
```
Input: coins = [1], amount = 2
Output: 2
```

Constraints:
* 1 <= coins.length <= 12
* 1 <= coins[i] <= 2^31 - 1
* 0 <= amount <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount+1, -1);
        dp[0] = 0;
        if (amount == 0)
            return 0;
        for (int i = 1; i <= amount; i ++) {
            int mincoins = INT_MAX;
            for (int j = 0; j < coins.size(); j ++) {
                if (i - coins[j] >= 0) {
                    if (dp[i-coins[j]] != -1)
                        mincoins = min(mincoins, dp[i-coins[j]] + 1);
                }
            }
            if (mincoins != INT_MAX)
                dp[i] = mincoins;
        }
        return (dp[amount] == 0) ? -1 : dp[amount];
    }
};
```


