---
layout: post
title: "Find The Duplicate Number Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Two Pointers, Binary Search, Bit Manipulation ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 287. Given an array of integers nums containingn + 1 integers where each integer is in the range [1, n] inclusive.

---

<br />

## Description

LeetCode Problem 287.

Given an array of integers nums containingn + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return thisrepeatednumber.

You must solve the problem without modifying the array numsand uses only constant extra space.

Example 1:
```
Input: nums = [1,3,4,2,2]
Output: 2
```

Example 2:
```
Input: nums = [3,1,3,4,2]
Output: 3
```

Example 3:
```
Input: nums = [1,1]
Output: 1
```

Example 4:
```
Input: nums = [1,1,2]
Output: 1
```

Constraints:
* 1 <= n <= 10^5
* nums.length == n + 1
* 1 <= nums[i] <= n
* All the integers in nums appear only once except for precisely one integer which appears two or more times.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int len = nums.size(); 
        if (len == 0)
            return 0;
        
        int p1 = nums[0], p2 = nums[nums[0]];
        while (p1 != p2) {
            p1 = nums[p1];
            p2 = nums[nums[p2]];
        }
        p1 = 0;
        while (p1 != p2) {
            p1 = nums[p1];
            p2 = nums[p2];
        }
        return p1;
    }
};
```


