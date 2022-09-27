---
layout: post
title: "Maximum Length Of Repeated Subarray Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search, Dynamic Programming, Sliding Window ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 718. Given two integer arrays nums1 and nums2, return the maximum length of a subarray that appears in both arrays.

---

<br />

## Description

LeetCode Problem 718.

Given two integer arrays nums1 and nums2, return the maximum length of a subarray that appears in both arrays.
Example 1:
```
Input: nums1 = [1,2,3,2,1], nums2 = [3,2,1,4,7]
Output: 3
Explanation: The repeated subarray with maximum length is [3,2,1].
```

Example 2:
```
Input: nums1 = [0,0,0,0,0], nums2 = [0,0,0,0,0]
Output: 5
```

Constraints:
* 1 <= nums1.length, nums2.length <= 1000
* 0 <= nums1[i], nums2[i] <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findLength(vector<int>& A, vector<int>& B) {
        int l1 = A.size(), l2 = B.size();
        vector<vector<int>> dp(l1+1, vector<int>(l2+2, 0));
        
        int max_freq = 0;
        for (int i = 1; i <= l1; i ++) {
            for (int j = 1; j <= l2; j ++) {
                if (A[i-1] == B[j-1]) {
                    dp[i][j] = dp[i-1][j-1] + 1;
                } else {
                    dp[i][j] = 0;
                }
                max_freq = max(max_freq, dp[i][j]);
            }        
        }
        
        return max_freq;
    }
};
```


