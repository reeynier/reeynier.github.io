---
layout: post
title: "Maximum Product Of Three Numbers Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Sorting ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 628. Given an integer array nums, find three numbers whose product is maximum and return the maximum product.

---

<br />

## Description

LeetCode Problem 628.

Given an integer array nums, find three numbers whose product is maximum and return the maximum product.

Example 1:
```
Input: nums = [1,2,3]
Output: 6
```

Example 2:
```
Input: nums = [1,2,3,4]
Output: 24
```

Example 3:
```
Input: nums = [-1,-2,-3]
Output: -6
```

Constraints:
* 3 <= nums.length <=10^4
* -1000 <= nums[i] <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maximumProduct(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        return max(nums[n - 1] * nums[n - 2] * nums[n - 3], nums[0] * nums[1] * nums[n - 1]);
    }
};
```


