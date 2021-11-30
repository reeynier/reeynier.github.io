---
layout: post
title: "Best Time To Buy And Sell Stock Iii Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 123. You are given an array prices where prices[i] is the price of a given stock on the ith day.

---

<br />

## Description

LeetCode Problem 123.

You are given an array prices where prices[i] is the price of a given stock on the i^th day.
Find the maximum profit you can achieve. You may complete at most two transactions.

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

Example 1:
```
Input: prices = [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
```

Example 2:
```
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.
```

Example 3:
```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

Example 4:
```
Input: prices = [1]
Output: 0
```

Constraints:
* 1 <= prices.length <= 10^5
* 0 <= prices[i] <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    int MaxProfitDp(int[] prices) {
    	// DP formula:
    	// dp[k, i] = max(dp[k, i-1], prices[i] - prices[j] + dp[k-1, j-1]), j=[0..i-1]
        if (prices.Length == 0) return 0;
            var dp = new int[3, prices.Length];
        for (int k = 1; k <= 2; k++) {
            int min = prices[0];
            for (int i = 1; i < prices.Length; i++) {
                min = Math.Min(min, prices[i] - dp[k-1, i-1]);
                dp[k, i] = Math.Max(dp[k, i-1], prices[i] - min);
            }
        }

        return dp[2, prices.Length - 1];
    }
};
```


