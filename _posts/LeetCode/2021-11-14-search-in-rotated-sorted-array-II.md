---
layout: post
title:  "Search in Rotated Sorted Array II Problem"
categories: [ Algorithm ]
tags: [ Array, Binary Search, Leetcode ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 81. There is an integer array nums sorted in non-decreasing order (not necessarily with distinct values).
---

<br />

## Description

LeetCode Problem 81. 

There is an integer array nums sorted in non-decreasing order (not necessarily with distinct values).

Before being passed to your function, nums is rotated at an unknown pivot index k (0 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,4,4,5,6,6,7] might be rotated at pivot index 5 and become [4,5,6,6,7,0,1,2,4,4].

Given the array nums after the rotation and an integer target, return true if target is in nums, or false if it is not in nums.

You must decrease the overall operation steps as much as possible.

 

Example 1:
```
Input: nums = [2,5,6,0,0,1,2], target = 0
Output: true
```

Example 2:
```
Input: nums = [2,5,6,0,0,1,2], target = 3
Output: false
```

Constraints:

* 1 <= nums.length <= 5000
* -10^4 <= nums[i] <= 10^4
* nums is guaranteed to be rotated at some pivot.
* -10^4 <= target <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool search(vector<int>& A, int t) {
        if (A.empty()) 
            return false;
        
        int l = 0, r = A.size() - 1;
        
        while (l < r) {
            int m = l + (r - l) / 2;    
            if (A[m] == t) return true;
            if (A[l] < A[m]) {
                if (A[l] <= t && t < A[m]) {
                    r = m - 1;
                } else {
                    l = m + 1;
                }
            } else if (A[m] < A[r]) {
                if (A[m] < t && t <= A[r]) {
                    l = m + 1;
                } else {
                    r = m - 1;
                }
            } else {
                if (A[l] == A[m]) l++;
                if (A[m] == A[r]) r--;
            }
        }
        
        return A[l] == t? true : false;
    }
};
```
