---
layout: post
title: "Find Peak Element Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 162. A peak element is an element that is strictly greater than its neighbors.

---

<br />

## Description

LeetCode Problem 162.

A peak element is an element that is strictly greater than its neighbors.

Given an integer array nums, find a peak element, and return its index. Ifthe array contains multiple peaks, return the index to any of the peaks.

You may imagine that nums[-1] = nums[n] = -inf.

You must write an algorithm that runs inO(log n) time.

Example 1:
```
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

Example 2:
```
Input: nums = [1,2,1,3,5,6,4]
Output: 5
Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.
```

Constraints:
* 1 <= nums.length <= 1000
* -2^31 <= nums[i] <= 2^31 - 1
* nums[i] != nums[i + 1] for all valid i.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int len = nums.size();
        int left = 0, right = nums.size() - 1;
        int mid;
        while (left < right) {
            mid = (left + right) / 2;
            
            if ((mid < len-1 && nums[mid] > nums[mid+1]) && 
                (mid > 0 && nums[mid] > nums[mid-1])) 
                return mid;
            if (mid == 0 && nums[mid] > nums[mid+1])
                return mid;
            if (mid == len-1 && nums[mid] > nums[mid-1])
                return mid;

            if (mid < nums.size()-1 && nums[mid+1] > nums[mid])
                left = mid + 1;
            else
                right = mid;
            
        }
        return left;
    }
};
```


