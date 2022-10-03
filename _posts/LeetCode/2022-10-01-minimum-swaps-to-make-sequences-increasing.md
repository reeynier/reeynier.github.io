---
layout: post
title: "Minimum Swaps To Make Sequences Increasing Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 801. You are given two integer arrays of the same length nums1 and nums2. In one operation, you are allowed to swap nums1[i] with nums2[i].

---

<br />

## Description

LeetCode Problem 801.

You are given two integer arrays of the same length nums1 and nums2. In one operation, you are allowed to swap nums1[i] with nums2[i].

* For example, if nums1 = [1,2,3,8], and nums2 = [5,6,7,4], you can swap the element at i = 3 to obtain nums1 = [1,2,3,4] and nums2 = [5,6,7,8].

Return the minimum number of needed operations to make nums1 and nums2 strictly increasing.
 The test cases are generated so that the given input always makes it possible.

An array arr is strictly increasing if and only if arr[0] < arr[1] < arr[2] < ... < arr[arr.length - 1].

Example 1:
```
Input: nums1 = [1,3,5,4], nums2 = [1,2,3,7]
Output: 1
Explanation: 
Swap nums1[3] and nums2[3]. Then the sequences are:
nums1 = [1, 3, 5, 7] and nums2 = [1, 2, 3, 4]
which are both strictly increasing.
```

Example 2:
```
Input: nums1 = [0,3,5,8,9], nums2 = [2,1,4,6,9]
Output: 1
```

Constraints:
* 2 <= nums1.length <= 10^5
* nums2.length == nums1.length
* 0 <= nums1[i], nums2[i] <= 2 * 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    int minSwap(vector<int>& A, vector<int>& B) {
        int len = A.size();
        int no_swaps [1100] = {0};
        int swaps [1100] = {1};
        
        for (int i = 1; i < len; i ++) {
            no_swaps[i] = INT_MAX;
            swaps[i] = INT_MAX;
            if (A[i-1] < A[i] and B[i-1] < B[i]) {
                no_swaps[i] = no_swaps[i-1];
                swaps[i] = swaps[i-1] + 1;
            }
            if (A[i-1] < B[i] and B[i-1] < A[i]) {
                no_swaps[i] = min(no_swaps[i], swaps[i-1]);
                swaps[i] = min(no_swaps[i-1]+1, swaps[i]);
            }
        }
        return min(no_swaps[len-1], swaps[len-1]);
    }
};
```


