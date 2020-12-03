---
layout: post
title:  "Median of Two Sorted Arrays Problem"
categories: [ Algorithm ]
tags: [ Binary Search, Leetcode ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 4. Given two sorted arrays **nums1** and **nums2** of size **m** and **n** respectively, return the median of the two sorted arrays.
---

<br />

## Description

LeetCode Problem 4. Given two sorted arrays **nums1** and **nums2** of size **m** and **n** respectively, return the median of the two sorted arrays.


Example: 
```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.

Input: num1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2+3)/2 = 2.5.
```

<br />

## Solution

#### Binary Search Approach

A simple `brute force` approach is to merge and then sort the two arrays. We can then find the median of the long single array. The time complexity and space complexity of this approach will be O(m+n).


We can use the `binary search` approach to speed up the search. We can use two pointers *c1* and *c2*, pointing at elements from the two arrays respectively. In the end, we would like to set these two pointers pointing at the median number(s) in the two arrays. 

When the two pointers pointing at the median number(s), there are two requirements need to be met:  
1. Length(left part of nums1) + Length(left part of nums2) = Length(right part of nums1) + Length(right part of nums2)
2. max(left part of nums1, left part of nums2) <= min(right part of nums1, right part of nums2)

where the left part refers to the subarray that is on the left side to the pointer, and the right part refers to the subarray that is on the right side to the pointer.

These two requirements guarantee that the elements pointed by the two pointers are the median number(s). As the two arrays are already sorted, to locate these two elements, we can use `binary search`. To simplify the search, we assume the length of the first array is larger than or equal to the length of the second array. (We swap the array if this is not the case.)

At the beginning, we set two pointers *l* and *r*, where *l* pointing at the index 0 of the first array, and *r* pointing at the index m-1 of the second array. Then we set *c1* to be the average value of *l* and *r* (*mid = (l+r)/2*). To meet the first requirement, we set *c2* to be *half-mid*, where *half* is the half length of the merged array (*half = (m+n)/2*). Then we can be sure that the numbers on the left side to *c1* and *c2* equals the numbers on the right side.

Then we need to check whether the second requirement is met. To check this, we need four numbers: max of left part of nums1, max of left part of nums2, min of right part of nums1, and min of right part of nums2. These four numbers are nums1[c1-1], nums2[c2-1], nums1[c1], nums2[c2] respectively.

If max(nums1[c1-1], nums2[c2-1]) <= min(nums1[c1], nums2[c2]), the second requirement is met, then we are done. We can break from the binary search.

Otherwise, we keep on searching. We need to make sure if *c1* is too big or too small. We check if nums1[c1-1] < nums2[c2-1], that means *c1* is pointing at an element too small for a median. Then we increase the left pointer *l*. If nums1[c1-1] >= nums2[c2-1], that means *c1* is pointing at an element too big for a median. Then we decrease the right pointer *r*. 

We repeat the above steps until the left pointer *l* is greater than or equal to the right pointer *r*. Then we can return the median of the two sorted arrays.


<br />

## Sample C++ Code

This is a C++ implementation of the binary search approach.

```c
#include <iostream>
#include <algorithm>
#include <vector>
#include <climits>

using namespace std;

double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    // make sure nums1.size() >= nums2.size(), otherwise, we swap the two arrays
    if (nums1.size() < nums2.size()) {
        auto temp = nums1;
        nums1 = nums2;
        nums2 = temp;
    }
    int m = nums1.size();
    int n = nums2.size();
    int half = (m + n) / 2;
    
    // some initial settings
    int l = 0, r = m, mid;
    int c1, c2, p1, p2, q1, q2;
    q1 = (m > 0) ? nums1[0] : INT_MAX;
    q2 = (n > 0) ? nums2[0] : INT_MAX;

    // binary search
    while (l < r) {
        mid = (l+r) / 2;
        c1 = mid, c2 = half-mid;
        if (c1 > half) {
            r = mid; continue;
        } else if (c2 > n) {
            l = mid; continue;
        }
        
        p1 = INT_MIN, p2 = INT_MIN;
        if (c1 > 0) p1 = nums1[c1-1];
        if (c2 > 0) p2 = nums2[c2-1];
        
        q1 = INT_MAX, q2 = INT_MAX;
        if (c1 < m) q1 = nums1[c1];
        if (c2 < n) q2 = nums2[c2];
        
        if (max(p1, p2) <= min(q1, q2)) {
            break;
        } else if (p1 < p2) {
            l = mid + 1;
        } else {
            r = mid;
        }
    }
    
    // calculate median
    double ans;
    if ((m + n) % 2 == 0) {
        ans = ((double)(max(p1, p2)) + (double)(min(q1, q2)))/2;
    } else {
        ans = (double)(min(q1, q2));
    }
    return ans;
}

int main() {
    vector<int> nums1 = {1, 3};
    vector<int> nums2 = {2};
    cout << findMedianSortedArrays(nums1, nums2) << endl;
}
```
