---
layout: post
title: "Cheapest Flights Within K Stops Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming, Depth-First Search, Breadth-First Search, Graph, Heap, Shortest Path ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 787. There are n cities connected by some number of flights. You are given an array flights where flights[i] = [from_i, to_i, price_i] indicates that there is a flight from city from_i to city to_i with cost price_i.

---

<br />

## Description

LeetCode Problem 787.

There are n cities connected by some number of flights. You are given an array flights where flights[i] = [from_i, to_i, price_i] indicates that there is a flight from city from_i to city to_i with cost price_i.

You are also given three integers src, dst, and k, return the cheapest price from src to dst with at most k stops. If there is no such route, return -1.

Example 1: 
```
Input: n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 1
Output: 200
Explanation: The graph is shown.
The cheapest price from city 0 to city 2 with at most 1 stop costs 200, as marked red in the picture.
```

Example 2: 
```
Input: n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 0
Output: 500
Explanation: The graph is shown.
The cheapest price from city 0 to city 2 with at most 0 stop costs 500, as marked blue in the picture.
```

Constraints:
* 1 <= n <= 100
* 0 <= flights.length <= (n * (n - 1) / 2)
* flights[i].length == 3
* 0 <= from_i, to_i < n
* from_i != to_i
* 1 <= price_i <= 10^4
* There will not be any multiple flights between two cities.
* 0 <= src, dst, k < n
* src != dst

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int K) {
        vector<vector<int>> dp(K + 2, vector<int> (n, INT_MAX));
        for (int i = 0; i <= K + 1; i++) 
            dp[i][src] = 0;
        for (int i = 1; i <= K + 1; i++) {
            for (auto& f : flights) {
                if (dp[i-1][f[0]] != INT_MAX)
                  dp[i][f[1]] = min(dp[i][f[1]], dp[i-1][f[0]] + f[2]);
            }
        }
        return dp[K+1][dst] == INT_MAX ? - 1 : dp[K+1][dst];
    }
};
```


