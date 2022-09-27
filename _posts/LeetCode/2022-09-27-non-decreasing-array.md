---
layout: post
title: "Non-Decreasing Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 665. Given an array nums with n integers, your task is to check if it could become non-decreasing by modifying at most one element.

---

<br />

## Description

LeetCode Problem 665.

Given an array nums with n integers, your task is to check if it could become non-decreasing by modifying at most one element.

We define an array is non-decreasing if nums[i] <= nums[i + 1] holds for every i (0-based) such that (0 <= i <= n - 2).

Example 1:
```
Input: nums = [4,2,3]
Output: true
Explanation: You could modify the first 4 to 1 to get a non-decreasing array.
```

Example 2:
```
Input: nums = [4,2,1]
Output: false
Explanation: You can't get a non-decreasing array by modify at most one element.
```

Constraints:
* n == nums.length
* 1 <= n <= 10^4
* -10^5 <= nums[i] <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool checkPossibility(vector<int>& nums) {
        for (int i = 0; i < nums.size() - 1; i++) {
            if (nums[i] > nums[i + 1]) {
                if (i - 1 >= 0 && nums[i - 1] > nums[i + 1]) 
                    nums[i + 1] = nums[i];
                else 
                    nums[i] = nums[i + 1];
                break;
            }
        }
        for (int i = 0; i < nums.size() - 1; i++) {
            if (nums[i] > nums[i + 1])
                return false;
        }
        return true; 
    }
};
```


