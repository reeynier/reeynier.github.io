---
layout: post
title: "Minimum Size Subarray Sum Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search, Sliding Window, Prefix Sum ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 209. Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [nums_l, nums_l+1, ..., nums_r-1, nums_r] of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.

---

<br />

## Description

LeetCode Problem 209.

Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [nums_l, nums_l+1, ..., nums_r-1, nums_r] of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.

Example 1:
```
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
```

Example 2:
```
Input: target = 4, nums = [1,4,4]
Output: 1
```

Example 3:
```
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
```

Constraints:
* 1 <= target <= 10^9
* 1 <= nums.length <= 10^5
* 1 <= nums[i] <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    int minSubArrayLen(int s, vector<int>& nums) {
        if (nums.size() == 0)
            return 0;
        int minlen = INT_MAX;
        int sum = 0;
        int left = 0;
        for (int i = 0; i < nums.size(); i ++) {
            sum += nums[i];
            while (sum >= s) {
                if (sum - nums[left] >= s) {
                    sum -= nums[left];
                    left ++;
                }
                else {
                    break;
                }
            }
            if (sum >= s)
                minlen = min(minlen, i - left + 1);
        }
        if (minlen == INT_MAX)
            return 0;
        else
            return minlen;
    }
};
```


