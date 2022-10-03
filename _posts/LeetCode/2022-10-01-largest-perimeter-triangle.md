---
layout: post
title: "Largest Perimeter Triangle Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Greedy, Sorting ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 976. Given an integer array nums, return the largest perimeter of a triangle with a non-zero area, formed from three of these lengths. If it is impossible to form any triangle of a non-zero area, return 0.

---

<br />

## Description

LeetCode Problem 976.

Given an integer array nums, return the largest perimeter of a triangle with a non-zero area, formed from three of these lengths. If it is impossible to form any triangle of a non-zero area, return 0.

Example 1:
```
Input: nums = [2,1,2]
Output: 5
```

Example 2:
```
Input: nums = [1,2,1]
Output: 0
```

Example 3:
```
Input: nums = [3,2,3,4]
Output: 10
```

Example 4:
```
Input: nums = [3,6,2,3]
Output: 8
```

Constraints:
* 3 <= nums.length <= 10^4
* 1 <= nums[i] <= 10^6

<br />

## Sample C++ Code


```c
class Solution {
public:
    int largestPerimeter(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        for (int i = nums.size()-3; i >= 0; i--) {
            if (nums[i] + nums[i+1] > nums[i+2])
                return nums[i] + nums[i+1] + nums[i+2];
        }
        return 0;
    }
};
```


