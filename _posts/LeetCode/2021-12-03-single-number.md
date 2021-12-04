---
layout: post
title: "Single Number Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Bit Manipulation ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 136. Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

---

<br />

## Description

LeetCode Problem 136.

Given a non-emptyarray of integers nums, every element appears twice except for one. Find that single one.

You mustimplement a solution with a linear runtime complexity and useonly constantextra space.

Example 1:
```
Input: nums = [2,2,1]
Output: 1
```

Example 2:
```
Input: nums = [4,1,2,1,2]
Output: 4
```

Example 3:
```
Input: nums = [1]
Output: 1
```

Constraints:
* 1 <= nums.length <= 3 * 10^4
* -3 * 10^4 <= nums[i] <= 3 * 10^4
* Each element in the array appears twice except for one element which appears only once.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int n = 0;
        for (int i = 0; i < nums.size(); i ++) {
            n = n ^ (nums[i]);
        }    
        return n;
    }
};
```


