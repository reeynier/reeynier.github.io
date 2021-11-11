---
layout: post
title:  "Sort Colors Problem"
categories: [ Data Structure ]
tags: [ Array, Two Pointers, Leetcode ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 75. Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.
---

<br />

## Description

LeetCode Problem 75. 

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

 

Example 1:
```
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

Example 2:
```
Input: nums = [2,0,1]
Output: [0,1,2]
```

Example 3:
```
Input: nums = [0]
Output: [0]
```

Example 4:
```
Input: nums = [1]
Output: [1]
```
 

Constraints:

* n == nums.length
* 1 <= n <= 300
* nums[i] is 0, 1, or 2.

<br />

## Sample C++ Code


```c
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int p0 = 0, p2 = nums.size()-1;
        int curr = 0, tmp;
        while (curr <= p2) {
            if (nums[curr] == 0) {
                tmp = nums[curr];
                nums[curr] = nums[p0];
                nums[p0] = tmp;
                curr ++;
                p0 ++;
            } else if (nums[curr] == 2) {
                tmp = nums[curr];
                nums[curr] = nums[p2];
                nums[p2] = tmp;
                p2 --;
            } else {
                curr ++;
            }
        }
        return;
    }
};
```
