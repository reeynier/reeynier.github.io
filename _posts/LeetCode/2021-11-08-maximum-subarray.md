---
layout: post
title:  "Maximum Subarray Problem"
categories: [ Algorithm ]
tags: [ Array, Divide and Conquer, Dynamic Programming, Leetcode ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 53. Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
---

<br />

## Description

LeetCode Problem 53. 

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

 

Example 1:
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

Example 2:
```
Input: nums = [1]
Output: 1
```

Example 3:
```
Input: nums = [5,4,-1,7,8]
Output: 23
```

Constraints:

* 1 <= nums.length <= 10^5
* -10^4 <= nums[i] <= 10^4


<br />

## Sample C++ Code


```c
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        if (nums.size() == 0)
            return 0;
        int max_sum = nums[0];
        for (int i = 1; i < nums.size(); i ++) {
            if (nums[i-1] > 0)
                nums[i] += nums[i-1];
        }
        for (int i = 0; i < nums.size(); i ++) {
            if (nums[i] > max_sum)
                max_sum = nums[i];
        }
        return max_sum;
    }
};
```
