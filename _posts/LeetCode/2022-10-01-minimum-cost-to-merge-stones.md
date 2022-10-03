---
layout: post
title: "Minimum Cost To Merge Stones Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 1000. There are n piles of stones arranged in a row. The i^th pile has stones[i] stones.

---

<br />

## Description

LeetCode Problem 1000.

There are n piles of stones arranged in a row. The i^th pile has stones[i] stones.

A move consists of merging exactly k consecutive piles into one pile, and the cost of this move is equal to the total number of stones in these k piles.

Return the minimum cost to merge all piles of stones into one pile. If it is impossible, return -1.

Example 1:
```
Input: stones = [3,2,4,1], k = 2
Output: 20
Explanation: We start with [3, 2, 4, 1].
We merge [3, 2] for a cost of 5, and we are left with [5, 4, 1].
We merge [4, 1] for a cost of 5, and we are left with [5, 5].
We merge [5, 5] for a cost of 10, and we are left with [10].
The total cost was 20, and this is the minimum possible.
```

Example 2:
```
Input: stones = [3,2,4,1], k = 3
Output: -1
Explanation: After any merge operation, there are 2 piles left, and we can't merge anymore.  So the task is impossible.
```

Example 3:
```
Input: stones = [3,5,1,2,6], k = 3
Output: 25
Explanation: We start with [3, 5, 1, 2, 6].
We merge [5, 1, 2] for a cost of 8, and we are left with [3, 8, 6].
We merge [3, 8, 6] for a cost of 17, and we are left with [17].
The total cost was 25, and this is the minimum possible.
```

Constraints:
* n == stones.length
* 1 <= n <= 30
* 1 <= stones[i] <= 100
* 2 <= k <= 30

<br />

## Sample C++ Code


```c
class Solution {
public:
    int dp[31][31];
    int solve(vector<int>&arr, int k, int left, int right) {
        
        if (dp[left][right] != 100000) 
            return dp[left][right];
        
        if (right - left < k) {
            dp[left][right] = 0;
            return dp[left][right];
        }
        
        int sum = 0;
		
		// base case. returns the cost to merge initial K piles of stones.
        if (right - left == k) {    
            for (int i = left; i < right; i++) {
                sum += arr[i];
            }
            dp[left][right] = sum;
            return dp[left][right];
        }
        
        int res = 1000000;
        
        // calculate the Cost for any applicable subarray, per recursive call.
        if ((right - left - 1) % (k - 1) == 0)
            for (int i = left; i < right; i++) {
                sum += arr[i];
            }
        
        for(int i = left + 1; i < right; i += k - 1) {
        	// recursively calculates the minimal value for every subarray
            res = min(res, solve(arr, k, left, i) + solve(arr, k, i, right));
        }
		
        // update the minimal cost of sub-subarrays with the actual cost of the subarray
        dp[left][right] = sum + res;
        return dp[left][right];
    }
    
    int mergeStones(vector<int>& stones, int k) {
        if ((stones.size() - 1) % (k - 1) != 0) 
            return -1;
        
        for (int i = 0; i < 31; i++) {
            for (int j = 0; j < 31; j++) {
                dp[i][j] = 100000;
            }
        }
        
        return solve(stones, k, 0, stones.size());
    }
};
```


