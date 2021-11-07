---
layout: post
title:  "3Sum Closest Problem"
categories: [ Data Structure ]
tags: [ Array, Two Pointers, Sorting, Leetcode ]
similar: [ Sorting ]
featured: false
hidden: false
excerpt: LeetCode 16. Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.
---

<br />

## Description

LeetCode Problem 16. 

Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.

Return the sum of the three integers.

You may assume that each input would have exactly one solution.

 

Example 1:
```
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

Example 2:
```
Input: nums = [0,0,0], target = 1
Output: 0
```
 

Constraints:

* 3 <= nums.length <= 1000
* -1000 <= nums[i] <= 1000
* -10^4 <= target <= 10^4



<br />

## Sample C++ Code


```c
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());
        int n = nums.size(), ans = nums[0] + nums[1] + nums[2];
        for (int i = 0; i < n-2; ++i) {
            int l = i + 1, r = n - 1;
            while (l < r) {
                int sum3 = nums[i] + nums[l] + nums[r];
                if (abs(ans - target) > abs(sum3 - target)) // Update better ans
                    ans = sum3;
                if (sum3 == target) break;
                if (sum3 > target)
                    // Sum3 is greater than the target, to minimize the difference, we have to decrease our sum3
                    --r; 
                else
                    // Sum3 is lesser than the target, to minimize the difference, we have to increase our sum3
                    ++l; 
            }
        }
        return ans;
    }
};
```
