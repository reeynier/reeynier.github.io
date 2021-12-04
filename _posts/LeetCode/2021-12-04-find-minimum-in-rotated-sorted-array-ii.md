---
layout: post
title: "Find Minimum In Rotated Sorted Array II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 154. Suppose an array of length n sorted in ascending order is rotated between 1 and n times. 

---

<br />

## Description

LeetCode Problem 154.

Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,4,4,5,6,7] might become:
* [4,5,6,7,0,1,4] if it was rotated 4 times.
* [0,1,4,4,5,6,7] if it was rotated 7 times.

Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].

Given the sorted rotated array nums that may contain duplicates, return the minimum element of this array.
You must decrease the overall operation steps as much as possible.

Example 1:
```
Input: nums = [1,3,5]
Output: 1
```

Example 2:
```
Input: nums = [2,2,2,0,1]
Output: 0
```

Constraints:
* n == nums.length
* 1 <= n <= 5000
* -5000 <= nums[i] <= 5000
* nums is sorted and rotated between 1 and n times.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findMin(vector<int> &num) {
        int l = 0,r = num.size() - 1,mid = 0;
        while(l < r) {
            mid = l + (r - l) / 2;           
            if (num[mid] > num[r]) l = mid + 1;
            else if (num[mid] < num[r]) r = mid;
            else r--;
        }
        return num[l];
    }
};
```


