---
layout: post
title: "Partition Array Into Disjoint Intervals Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 915. Given an integer array nums, partition it into two (contiguous) subarrays left and right so that

---

<br />

## Description

LeetCode Problem 915.

Given an integer array nums, partition it into two (contiguous) subarrays left and right so that:
* Every element in left is less than or equal to every element in right.
* left and right are non-empty.
* left has the smallest possible size.

Return the length of left after such a partitioning.

Test cases are generated such that partitioning exists.

Example 1:
```
Input: nums = [5,0,3,8,6]
Output: 3
Explanation: left = [5,0,3], right = [8,6]
```

Example 2:
```
Input: nums = [1,1,1,0,6,12]
Output: 4
Explanation: left = [1,1,1,0], right = [6,12]
```

Constraints:
* 2 <= nums.length <= 10^5
* 0 <= nums[i] <= 10^6
* There is at least one valid answer for the given input.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int partitionDisjoint(vector<int>& a) {
        int minNum = a[0], maxNum = a[0];
        int index = 0;
        for (int i = 1; i < a.size(); i++) {
            if (a[i] < minNum) {
                index = i;
                minNum = maxNum;
            }
            maxNum = max(a[i], maxNum);
        }
        return index + 1;
    }
};
```


