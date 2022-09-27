---
layout: post
title: "Number Of Subarrays With Bounded Maximum Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Two Pointers ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 795. Given an integer array nums and two integers left and right, return the number of contiguous non-empty subarrays such that the value of the maximum array element in that subarray is in the range [left, right].

---

<br />

## Description

LeetCode Problem 795.

Given an integer array nums and two integers left and right, return the number of contiguous non-empty subarrays such that the value of the maximum array element in that subarray is in the range [left, right].

The test cases are generated so that the answer will fit in a 32-bit integer.

Example 1:
```
Input: nums = [2,1,4,3], left = 2, right = 3
Output: 3
Explanation: There are three subarrays that meet the requirements: [2], [2, 1], [3].
```

Example 2:
```
Input: nums = [2,9,2,5,6], left = 2, right = 8
Output: 7
```

Constraints:
* 1 <= nums.length <= 10^5
* 0 <= nums[i] <= 10^9
* 0 <= left <= right <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    int numSubarrayBoundedMax(vector<int>& A, int L, int R) {
        int result = 0, left = -1, right = -1;
        for (int i = 0; i < A.size(); i++) {
            if (A[i] > R) left = i;
            if (A[i] >= L) right = i;
            result += right - left;
        }
        return result;
    }
};
```


