---
layout: post
title: "Longest Increasing Subsequence Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 300. Given an integer array nums, return the length of the longest strictly increasing subsequence.

---

<br />

## Description

LeetCode Problem 300.

Given an integer array nums, return the length of the longest strictly increasing subsequence.

A subsequence is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, [3,6,2,7] is a subsequence of the array [0,3,1,6,2,2,7].

Example 1:
```
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
```

Example 2:
```
Input: nums = [0,1,0,3,2,3]
Output: 4
```

Example 3:
```
Input: nums = [7,7,7,7,7,7,7]
Output: 1
```

Constraints:
* 1 <= nums.length <= 2500
* -10^4 <= nums[i] <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int len = nums.size();
        vector<int> dp(len, 0);
        
        int ans = 0;
        for (int i = 0; i < len; i ++) {
            for (int j = 0; j < i; j ++) {
                if (nums[j] < nums[i]) 
                    dp[i] = max(dp[i], dp[j] + 1);
            }
            ans = max(ans, dp[i]);
        }
        
        return ans;
    }
};
```


