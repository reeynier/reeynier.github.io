---
layout: post
title: "Largest Sum Of Averages Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 813. You are given an integer array nums and an integer k. You can partition the array into at most k non-empty adjacent subarrays. The score of a partition is the sum of the averages of each subarray.

---

<br />

## Description

LeetCode Problem 813.

You are given an integer array nums and an integer k. You can partition the array into at most k non-empty adjacent subarrays. The score of a partition is the sum of the averages of each subarray.

Note that the partition must use every integer in nums, and that the score is not necessarily an integer.
Return the maximum score you can achieve of all the possible partitions. Answers within 10^-6 of the actual answer will be accepted.

Example 1:
```
Input: nums = [9,1,2,3,9], k = 3
Output: 20.00000
Explanation: 
The best choice is to partition nums into [9], [1, 2, 3], [9]. The answer is 9 + (1 + 2 + 3) / 3 + 9 = 20.
We could have also partitioned nums into [9, 1], [2], [3, 9], for example.
That partition would lead to a score of 5 + 2 + 6 = 13, which is worse.
```

Example 2:
```
Input: nums = [1,2,3,4,5,6,7], k = 4
Output: 20.50000
```

Constraints:
* 1 <= nums.length <= 100
* 1 <= nums[i] <= 10^4
* 1 <= k <= nums.length

<br />

## Sample C++ Code


```c
class Solution {
public:
    int n;
    vector<int> pre;
    double dfs(int curr, int k, vector<int>&nums, vector<vector<double>>&dp) {
        if (curr == n && k != 0) 
            return 0;
        if (k == 0) {
            return curr != 0 ? (double)(pre[n-1]-pre[curr-1]) / (n-curr) : (double)(pre[n-1]) / n;
        }
        if (dp[curr][k] != -1) 
            return dp[curr][k];
        double ans = 0, sum = 0;
        for (int i = curr; i < n - k; i++) {
            sum += nums[i];
            ans = max(ans, (double)sum / (i+1-curr) + dfs(i+1, k-1, nums, dp));
        }
        return dp[curr][k] = ans;
    }
    double largestSumOfAverages(vector<int>& nums, int k) {
        n = nums.size();
        pre = nums;
        for (int i = 1; i < n; i++) 
            pre[i] += pre[i-1];
        vector<vector<double>> dp(n, vector<double>(k, -1));
        return dfs(0, k-1, nums, dp);
    }
};
```


