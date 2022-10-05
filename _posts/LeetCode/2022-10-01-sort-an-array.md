---
layout: post
title: "Sort An Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Divide and Conquer, Sorting, Heap, Merge Sort ]
similar: [ Sorting ]
featured: false
hidden: false
excerpt: LeetCode 912. Given an array of integers nums, sort the array in ascending order.

---

<br />

## Description

LeetCode Problem 912.

Given an array of integers nums, sort the array in ascending order.

Example 1:
```
Input: nums = [5,2,3,1]
Output: [1,2,3,5]
```

Example 2:
```
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
```

Constraints:
* 1 <= nums.length <= 5 * 10^4
* -5 * 10^4 <= nums[i] <= 5 * 10^4

<br />

## Sample C++ Code using Quick Sort

```c
class Solution {
public:
    int partition(vector<int> &nums, int i, int j) {
        int pivotIndex = i;
        int end = j;
        i++;
        while (i <= j) {
            while (i <= end && nums[i] < nums[pivotIndex]) i++;
            while (j >= pivotIndex && nums[j] > nums[pivotIndex]) j--;
            if (i <= j) {
                swap(nums[i++], nums[j--]);
            }
        }
        swap(nums[pivotIndex], nums[j]);
        return j;
    }
    
    void quickSort(vector<int> &nums, int l, int r) {
        if (l < r) {
            // swapping element at index l with element at random index
            swap(nums[l + rand() % (r -l + 1)], nums[l]);
            int mid = partition(nums, l, r);
            quickSort(nums, l, mid - 1);
            quickSort(nums, mid + 1, r);
        }
    }
    
    vector<int> sortArray(vector<int>& nums) {
        quickSort(nums, 0, nums.size()-1);
        return nums;
    }
};
```

