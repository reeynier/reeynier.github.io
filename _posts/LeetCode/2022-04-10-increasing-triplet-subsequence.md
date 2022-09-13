---
layout: post
title: "Increasing Triplet Subsequence Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Greedy ]
similar: [ Greedy ]
featured: false
hidden: false
excerpt: LeetCode 334. Given an integer array nums, return true if there exists a triple of indices (i, j, k) such that i < j < k and nums[i] < nums[j] < nums[k]. If no such indices exists, return false.

---

<br />

## Description

LeetCode Problem 334.

Given an integer array nums, return true if there exists a triple of indices (i, j, k) such that i < j < k and nums[i] < nums[j] < nums[k]. If no such indices exists, return false.

Example 1:
```
Input: nums = [1,2,3,4,5]
Output: true
Explanation: Any triplet where i < j < k is valid.
```

Example 2:
```
Input: nums = [5,4,3,2,1]
Output: false
Explanation: No triplet exists.
```

Example 3:
```
Input: nums = [2,1,5,0,4,6]
Output: true
Explanation: The triplet (3, 4, 5) is valid because nums[3] == 0 < nums[4] == 4 < nums[5] == 6.
```

Constraints:
* 1 <= nums.length <= 5 * 10^5
* -2^31 <= nums[i] <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool increasingTriplet(vector<int>& nums) {
        int len = nums.size();
        
        if (len < 3)
            return false;
        
        int a = INT_MAX, b = INT_MAX;
        
        for (int i = 0; i < len; i ++) {
            if (nums[i] <= a)
                a = nums[i];
            else if (nums[i] <= b)
                b = nums[i];
            else 
                return true;
        }
        return false;
    }
};
```


