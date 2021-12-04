---
layout: post
title: "Best Time To Buy And Sell Stock IV Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 188. You are given an integer array prices where prices[i] is the price of a given stock on the i^th day, and an integer k.

---

<br />

## Description

LeetCode Problem 188.

You are given an integer array prices where prices[i] is the price of a given stock on the i^th day, and an integer k.

Find the maximum profit you can achieve. You may complete at most k transactions.

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

Example 1:
```
Input: k = 2, prices = [2,4,1]
Output: 2
Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.
```

Example 2:
```
Input: k = 2, prices = [3,2,6,5,0,3]
Output: 7
Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4. Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
```

Constraints:
* 0 <= k <= 100
* 0 <= prices.length <= 1000
* 0 <= prices[i] <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int maxProfit=0;
        
        if (prices.size()<2)
            return 0;
        if (k>prices.size()/2) {
            for (int i=1; i<prices.size(); i++)
                maxProfit += max(prices[i]-prices[i-1], 0);
            return maxProfit;
        }
        
        int hold[k+1];
        int rele[k+1];
        for (int i=0;i<=k;++i) {
            hold[i] = INT_MAX;
            rele[i] = 0;
        }
        
        for (int i=0; i<prices.size(); i++) {
            for (int j=k; j>=1; j--) {
                rele[j] = max(rele[j], prices[i]-hold[j]);
                hold[j] = min(hold[j], prices[i]-rele[j-1]);
                maxProfit = max(maxProfit, rele[j]);
            }
        }
        return maxProfit;
    }
};
```


