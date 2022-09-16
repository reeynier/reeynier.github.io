---
layout: post
title: "Move Zeroes Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Two Pointers ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 283. Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

---

<br />

## Description

LeetCode Problem 283.

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

Example 1:
```
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
```

Example 2:
```
Input: nums = [0]
Output: [0]
```

Constraints:
* 1 <= nums.length <= 10^4
* -2^31 <= nums[i] <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int len = nums.size();
        int i = 0, j = 0;
        for (i = 0; i < len; i ++) {
            if (nums[i] != 0) {
                nums[j] = nums[i];
                j ++;
            }
        }
        while (j < len) {
            nums[j] = 0;
            j ++;
        }
        return;
    }
};
```


