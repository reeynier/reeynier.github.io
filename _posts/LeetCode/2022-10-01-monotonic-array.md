---
layout: post
title: "Monotonic Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 896. An array is monotonic if it is either monotone increasing or monotone decreasing.

---

<br />

## Description

LeetCode Problem 896.

An array is monotonic if it is either monotone increasing or monotone decreasing.

An array nums is monotone increasing if for all i <= j, nums[i] <= nums[j]. An array nums is monotone decreasing if for all i <= j, nums[i] >= nums[j].

Given an integer array nums, return true if the given array is monotonic, or false otherwise.

Example 1:
```
Input: nums = [1,2,2,3]
Output: true
```

Example 2:
```
Input: nums = [6,5,4,4]
Output: true
```

Example 3:
```
Input: nums = [1,3,2]
Output: false
```

Example 4:
```
Input: nums = [1,2,4,5]
Output: true
```

Example 5:
```
Input: nums = [1,1,1]
Output: true
```

Constraints:
* 1 <= nums.length <= 10^5
* -10^5 <= nums[i] <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isMonotonic(vector<int>& A) {
        bool increase = true;
        bool decrease = true;
        for (int i = 0; i < A.size() - 1; i++) {
            if (A[i] > A[i+1]) 
                increase = false;
            if (A[i] < A[i+1]) 
                decrease = false;
            if (increase == false && decrease == false) 
                return false;
        }
        return true;
    }
};
```


