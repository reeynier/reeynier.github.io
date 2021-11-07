---
layout: post
title:  "Jump Game II Problem"
categories: [ Data Structure ]
tags: [ Array, Dynamic Programming, Greedy, Leetcode ]
similar: [ Greedy ]
featured: false
hidden: false
excerpt: LeetCode 45. Given an array of non-negative integers nums, you are initially positioned at the first index of the array.
---

<br />

## Description

LeetCode Problem 45. 

Given an array of non-negative integers nums, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

 

Example 1:
```
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

Example 2:
```
Input: nums = [2,3,0,1,4]
Output: 2
```

Constraints:

* 1 <= nums.length <= 10^4
* 0 <= nums[i] <= 1000


<br />

## Sample C++ Code


```c
class Solution {
public:
    int jump(vector<int>& nums) {
        int i = 0, n = nums.size(), step = 0, end = 0, maxend = 0;
        while (end < n - 1) {
            step++;
            for (;i <= end; i++) {
                maxend = max(maxend, i + nums[i]);
                if (maxend >= n - 1) return step;
            }
            if(end == maxend) break;
            end = maxend;
        }
        return n == 1 ? 0 : -1;
    }
};
```
