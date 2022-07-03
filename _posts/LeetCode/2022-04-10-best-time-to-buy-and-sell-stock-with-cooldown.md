---
layout: post
title: "Best Time To Buy And Sell Stock With Cooldown Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 309. You are given an array prices where prices[i] is the price of a given stock on the i^th day.

---

<br />

## Description

LeetCode Problem 309.

You are given an array prices where prices[i] is the price of a given stock on the i^th day.

Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restrictions:

* After you sell your stock, you cannot buy stock on the next day (i.e., cooldown one day).

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

Example 1:
```
Input: prices = [1,2,3,0,2]
Output: 3
Explanation: transactions = [buy, sell, cooldown, buy, sell]
```

Example 2:
```
Input: prices = [1]
Output: 0
```

Constraints:
* 1 <= prices.length <= 5000
* 0 <= prices[i] <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maxProfit(vector<int>& prices) {
	    vector<vector<int>> dp(prices.size()+2, vector<int>(2));
	    for(int i=prices.size()-1; i>=0; i--){
	        for(int j=0; j<=1; j++){
	            if(j){
	                dp[i][j] = max(-prices[i]+dp[i+1][0], dp[i+1][1]);
	            }
	            else{
	                dp[i][j] = max(prices[i]+dp[i+2][1], dp[i+1][0]);
	            }
	        }
	    }
	    return dp[0][1];
	}
};
```


