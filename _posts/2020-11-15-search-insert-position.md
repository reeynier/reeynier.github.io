---
layout: post
title:  "Search Insert Position Problem"
categories: [ Algorithm ]
tags: [ Binary Search, Leetcode ]
similar: [ Binary Search ]
featured: false
hidden: false
---

<br />

## Description

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.



Examples: 
```
Input: nums = [1,3,5,6], target = 5
Output: 2

Input: nums = [1,3,5,6], target = 2
Output: 1

Input: nums = [1,3,5,6], target = 7
Output: 4

Input: nums = [1,3,5,6], target = 0
Output: 0
```

<br />

## Solution

#### Binary Search Approach

A simple `brute force` approach is to enumerate all possible indices, and check which one is can be the position to insert. The time complexity of this approach is O(n).

As the array is already sorted, we can use `binary search` to speed up the search. We can use two pointers *l* and *r*. The left pointer *l* starts from index 0, and the right pointer *r* starts from index *l-1*, *l* is then length of the array. During each iteration, we calculate *m* to be the average of *l* and *r* (*m = (l + r) / 2*). If *nums[m] = target*, we can directly return *m*. If *nums[m] < target*, that means *m* is an index too small for insertion, we then set *l* to be *m + 1*. If *nums[m] > target*, that means *m* is an index too big for insertion, we then set *r* to be *m + 1*.

We continue the search until *l* is greater than *r*. Then we check whether *nums[m]* is greater than *target*. If so, we can insert *target* to the index *m*, as our binary search can make sure *nums[m-1]*, if exists, is smaller than *target*. Otherwise, we can insert *target* to the index *m + 1*, as our binary search can make sure *nums[m+1]*, if exists, is larger than *target*.

The time complexity of the binary search approach is O(logn), and the space complexity is O(1).

<br />

## Sample C++ Code

This is a C++ implementation of the binary search approach.

```c
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

int searchInsert(vector<int>& nums, int target) {
    int l, m, r;
    l = 0, r = nums.size() - 1;
    while (l <= r) {
        m = (l + r) / 2;
        if (nums[m] == target)
            return m;
        if (nums[m] < target) {
            l = m + 1;
        }
        else {
            r = m - 1;
        }
    }
    if (nums[m] > target)
        return m;
    else
        return m + 1;
}

int main() {
    vector<int> nums = {1, 3, 5, 6};
    int target = 4;
    cout << searchInsert(nums, target) << endl;
}
```
