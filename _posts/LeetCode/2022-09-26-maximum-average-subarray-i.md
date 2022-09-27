---
layout: post
title: "Maximum Average Subarray I Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Sliding Window ]
similar: [ Sliding Window ]
featured: false
hidden: false
excerpt: LeetCode 643. You are given an integer array nums consisting of n elements, and an integer k.

---

<br />

## Description

LeetCode Problem 643.

You are given an integer array nums consisting of n elements, and an integer k.

Find a contiguous subarray whose length is equal to k that has the maximum average value and return this value. Any answer with a calculation error less than 10^-5 will be accepted.

Example 1:
```
Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12.75000
Explanation: Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75
```

Example 2:
```
Input: nums = [5], k = 1
Output: 5.00000
```

Constraints:
* n == nums.length
* 1 <= k <= n <= 10^5
* -10^4 <= nums[i] <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    double findMaxAverage(vector<int>& nums, int k) {
        double sum = 0, res = INT_MIN;
        for (int i = 0; i < nums.size(); i++) {
            if (i < k) 
                sum += nums[i];
            else {
                res = max(sum, res);
                sum += nums[i] - nums[i-k];
            }
        }
        res = max(sum, res);
        return res / k;
    }
};
```


