---
layout: post
title: "Valid Triangle Number Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Two Pointers, Binary Search, Greedy, Sorting ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 611. Given an integer array nums, return the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.

---

<br />

## Description

LeetCode Problem 611.

Given an integer array nums, return the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.

Example 1:
```
Input: nums = [2,2,3,4]
Output: 3
Explanation: Valid combinations are: 
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3
```

Example 2:
```
Input: nums = [4,2,3,4]
Output: 4
```

Constraints:
* 1 <= nums.length <= 1000
* 0 <= nums[i] <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int triangleNumber(vector<int>& nums) {
        int res = 0, n = nums.size();
        sort(nums.begin(), nums.end());
        for (int i = n-1; i >= 0; i--) {
            int lo = 0, hi = i-1;
            while (lo < hi) {
                if (nums[lo] + nums[hi] > nums[i]) {
                    res += hi - lo;
                    hi--;
                }
                else 
                    lo++;
            }
        }
        return res;
    }
};
```


