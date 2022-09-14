---
layout: post
title: "Kth Largest Element In An Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Divide and Conquer, Sorting, Heap, Quickselect ]
similar: [ Heap ]
featured: false
hidden: false
excerpt: LeetCode 215. Given an integer array nums and an integer k, return the k^th largest element in the array.

---

<br />

## Description

LeetCode Problem 215.

Given an integer array nums and an integer k, return the k^th largest element in the array.

Note that it is the k^th largest element in the sorted order, not the k^th distinct element.

Example 1:
```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
```

Example 2:
```
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```

Constraints:
* 1 <= k <= nums.length <= 10^4
* -10^4 <= nums[i] <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int> pq(nums.begin(), nums.end());
        for (int i = 0; i < k - 1; i++) {
            pq.pop();
        }
        return pq.top();
    }
};
```


