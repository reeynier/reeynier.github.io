---
layout: post
title: "Stone Game Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 877. Alice and Bob play a game with piles of stones. There are an even number of piles arranged in a row, and each pile has a positive integer number of stones piles[i].

---

<br />

## Description

LeetCode Problem 877.

Alice and Bob play a game with piles of stones. There are an even number of piles arranged in a row, and each pile has a positive integer number of stones piles[i].

The objective of the game is to end with the most stones. The total number of stones across all the piles is odd, so there are no ties.

Alice and Bob take turns, with Alice starting first. Each turn, a player takes the entire pile of stones either from the beginning or from the end of the row. This continues until there are no more piles left, at which point the person with the most stones wins.

Assuming Alice and Bob play optimally, return true if Alice wins the game, or false if Bob wins.

Example 1:
```
Input: piles = [5,3,4,5]
Output: true
Explanation: 
Alice starts first, and can only take the first 5 or the last 5.
Say she takes the first 5, so that the row becomes [3, 4, 5].
If Bob takes 3, then the board is [4, 5], and Alice takes 5 to win with 10 points.
If Bob takes the last 5, then the board is [3, 4], and Alice takes 4 to win with 9 points.
This demonstrated that taking the first 5 was a winning move for Alice, so we return true.
```

Example 2:
```
Input: piles = [3,7,2,3]
Output: true
```

Constraints:
* 2 <= piles.length <= 500
* piles.length is even.
* 1 <= piles[i] <= 500
* sum(piles[i]) is odd.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int dp[1005][1005];
    
    int f(int l, int r, vector <int> &piles) {
        if (l == r-1) 
            return max(piles[l], piles[r]);
        
        if (dp[l][r] != -1) 
            return dp[l][r];
        
        int ifleft = piles[l] + max(f(l+2, r, piles), f(l+1, r-1, piles));
        int ifright = piles[r] + max(f(l+1, r-1, piles), f(l, r-2, piles));
        
        return dp[l][r] = max(ifleft, ifright);
    }
    
    bool stoneGame(vector<int>& piles) {
        int l = 0, r = piles.size()-1;
        memset(dp, -1, sizeof(dp));
        int alex = f(l, r, piles);
        int sum = 0;
        for (int i = 0; i < piles.size(); i++) 
            sum += piles[i];

        return alex > (sum - alex);
    }
};
```


