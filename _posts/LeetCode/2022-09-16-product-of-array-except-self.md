---
layout: post
title: "Product Of Array Except Self Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Prefix Sum ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 238. Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

---

<br />

## Description

LeetCode Problem 238.

Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs inO(n)time and without using the division operation.

Example 1:
```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

Example 2:
```
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

Constraints:
* 2 <= nums.length <= 10^5
* -30 <= nums[i] <= 30
* The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        if (n == 0) return nums;
        
        vector<int> left(n), right(n);
        left[0] = nums[0], right[n-1] = nums[n-1];
        for (int i = 1; i < n; i ++) {
            left[i] = left[i-1] * nums[i];
            right[n-i-1] = right[n-i] * nums[n-i-1];
        }
        
        vector<int> ans(n, 1);
        for (int i = 0; i < n; i ++) {
            if (i > 0) {
                ans[i] = ans[i] * left[i-1];
            }
            if (i < n-1) {
                ans[i] = ans[i] * right[i+1];
            }
        }
        
        return ans;
    }
};
```


