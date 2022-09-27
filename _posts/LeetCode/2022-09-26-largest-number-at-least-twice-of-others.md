---
layout: post
title: "Largest Number At Least Twice Of Others Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Sorting ]
similar: [ Sorting ]
featured: false
hidden: false
excerpt: LeetCode 747. You are given an integer array nums where the largest integer is unique.

---

<br />

## Description

LeetCode Problem 747.

You are given an integer array nums where the largest integer is unique.

Determine whether the largest element in the array is at least twice as much as every other number in the array. If it is, return the index of the largest element, or return -1 otherwise.

Example 1:
```
Input: nums = [3,6,1,0]
Output: 1
Explanation: 6 is the largest integer.
For every other number in the array x, 6 is at least twice as big as x.
The index of value 6 is 1, so we return 1.
```

Example 2:
```
Input: nums = [1,2,3,4]
Output: -1
Explanation: 4 is less than twice the value of 3, so we return -1.
```

Example 3:
```
Input: nums = [1]
Output: 0
Explanation: 1 is trivially at least twice the value as any other number because there are no other numbers.
```

Constraints:
* 1 <= nums.length <= 50
* 0 <= nums[i] <= 100
* The largest element in nums is unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int dominantIndex(vector<int>& nums) {
        if (nums.size() < 2){
            return nums.size()-1;
        }
        int max1 = INT_MIN;
        int max2 = INT_MIN;
        int result = -1;
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] > max1) {
                result = i;
                max2 = max1;
                max1 = nums[i];
            } else if (nums[i] > max2) {
                max2 = nums[i];
            }
        }
        return max1 >= 2*max2 ? result : -1;
    }
};
```


