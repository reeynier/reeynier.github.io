---
layout: post
title: "Split Array With Same Average Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Dynamic Programming, Bit Manipulation, Bitmask ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 805. You are given an integer array nums.

---

<br />

## Description

LeetCode Problem 805.

You are given an integer array nums.

You should move each element of nums into one of the two arrays A and B such that A and B are non-empty, and average(A) == average(B).

Return true if it is possible to achieve that and false otherwise.

Note that for an array arr, average(arr) is the sum of all the elements of arr over the length of arr.

Example 1:
```
Input: nums = [1,2,3,4,5,6,7,8]
Output: true
Explanation: We can split the array into [1,4,5,8] and [2,3,6,7], and both of them have an average of 4.5.
```

Example 2:
```
Input: nums = [3,1]
Output: false
```

Constraints:
* 1 <= nums.length <= 30
* 0 <= nums[i] <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool splitArraySameAverage(vector<int>& nums) {
        int n = nums.size();
        int sum = accumulate(nums.begin(), nums.end(), 0);
        
        vector<int> dp(sum + 1);
        dp[0] = 1;
        
        for (int num: nums) {
            for (int s = sum; s >= num; s--) {
                if (dp[s - num])
                    dp[s] |= (dp[s - num] << 1);
            }
        }
        
        for (int len = 1; len < n; len++) {
            if ((sum * len) % n == 0) {
                int s = sum*len/n;
                if (dp[s] && (dp[s] & (1 << len)))
                   return true;                    
            }
        }
        return false;
    }
};
```


