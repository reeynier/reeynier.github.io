---
layout: post
title: "Max Consecutive Ones Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 485. Given a binary array nums, return the maximum number of consecutive 1's in the array.

---

<br />

## Description

LeetCode Problem 485.

Given a binary array nums, return the maximum number of consecutive 1's in the array.

Example 1:
```
Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.
```

Example 2:
```
Input: nums = [1,0,1,1,0,1]
Output: 2
```

Constraints:
* 1 <= nums.length <= 10^5
* nums[i] is either 0 or 1.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int n = nums.size();
        int maxones = 0;
        int currones = 0;
        for (int i = 0; i < n; i ++) {
            if (nums[i] == 1) {
                currones ++;
                maxones = max(maxones, currones);
            } else {
                currones = 0;
            }
        }
        return maxones;
    }
};
```


