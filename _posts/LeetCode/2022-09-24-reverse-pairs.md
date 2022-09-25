---
layout: post
title: "Reverse Pairs Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search, Divide and Conquer, Merge Sort ]
similar: [ Merge Sort ]
featured: false
hidden: false
excerpt: LeetCode 493. Given an integer array nums, return the number of reverse pairs in the array.

---

<br />

## Description

LeetCode Problem 493.

Given an integer array nums, return the number of reverse pairs in the array.

A reverse pair is a pair (i, j) where 0 <= i < j < nums.length and nums[i] > 2 * nums[j].

Example 1:
```
Input: nums = [1,3,2,3,1]
Output: 2
```

Example 2:
```
Input: nums = [2,4,3,5,1]
Output: 3
```

Constraints:
* 1 <= nums.length <= 5 * 10^4
* -2^31 <= nums[i] <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
private:
    int count;
   
    void checkCount(vector<int>& nums, int start, int mid, int end) {
        // two pointers;
        int l = start, r = mid + 1;
        while (l <= mid && r <= end) {
            if ((long)nums[l] > (long) 2 * nums[r]) {
                count += (mid - l + 1);
                r++;
            } else {
                l++;
            }
        }
       // worst case might be nlog(n) 
        sort(nums.begin() + start, nums.begin() + end + 1);
        return;
    }
    
    void mergeSort(vector<int>& nums, int start, int end) {
        if (start == end) return;
        
        int mid = (start + end)/2;
        mergeSort(nums,start, mid);
        mergeSort(nums,mid+1,end);
        
        checkCount(nums,start,mid,end);
        return;
    }
    
public:
    int reversePairs(vector<int>& nums) {
        if (!nums.size()) return 0;
        count = 0;
        mergeSort(nums,0,nums.size()-1);
        return count;
    }
};
```


