---
layout: post
title: "Array Nesting Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Depth-First Search ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 565. You are given an integer array nums of length n where nums is a permutation of the numbers in the range [0, n - 1].

---

<br />

## Description

LeetCode Problem 565.

You are given an integer array nums of length n where nums is a permutation of the numbers in the range [0, n - 1].

You should build a set s[k] = {nums[k], nums[nums[k]], nums[nums[nums[k]]], ... } subjected to the following rule:
* The first element in s[k] starts with the selection of the element nums[k] of index = k.
* The next element in s[k] should be nums[nums[k]], and then nums[nums[nums[k]]], and so on.
* We stop adding right before a duplicate element occurs in s[k].

Return the longest length of a set s[k].

Example 1:
```
Input: nums = [5,4,0,3,1,6,2]
Output: 4
Explanation: 
nums[0] = 5, nums[1] = 4, nums[2] = 0, nums[3] = 3, nums[4] = 1, nums[5] = 6, nums[6] = 2.
One of the longest sets s[k]:
s[0] = {nums[0], nums[5], nums[6], nums[2]} = {5, 6, 2, 0}
```

Example 2:
```
Input: nums = [0,1,2]
Output: 1
```

Constraints:
* 1 <= nums.length <= 10^5
* 0 <= nums[i] < nums.length
* All the values of nums are unique.

<br />

## Sample C++ Code

The idea is to, start from every number, find circles in those index-pointer-chains. Every time we find a set (a circle) mark every number as visited (-1) so that next time we won't step on it again.

```c
class Solution {
public:
    int arrayNesting(vector<int>& a) {
        size_t maxsize = 0;
        for (int i = 0; i < a.size(); i++) {
            size_t size = 0;
            for (int k = i; a[k] >= 0; size++) {
                int ak = a[k];
                a[k] = -1; // mark a[k] as visited;
                k = ak;
            }
            maxsize = max(maxsize, size);
        }

        return maxsize;
    }
};
```


