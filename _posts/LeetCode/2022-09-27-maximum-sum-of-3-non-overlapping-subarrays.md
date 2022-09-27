---
layout: post
title: "Maximum Sum Of 3 Non-Overlapping Subarrays Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 689. Given an integer array nums and an integer k, find three non-overlapping subarrays of length k with maximum sum and return them.

---

<br />

## Description

LeetCode Problem 689.

Given an integer array nums and an integer k, find three non-overlapping subarrays of length k with maximum sum and return them.

Return the result as a list of indices representing the starting position of each interal (0-indexed). If there are multiple answers, return the lexicographically smallest one.

Example 1:
```
Input: nums = [1,2,1,2,6,7,5,1], k = 2
Output: [0,3,5]
Explanation: Subarrays [1, 2], [2, 6], [7, 5] correspond to the starting indices [0, 3, 5].
We could have also taken [2, 1], but an answer of [1, 3, 5] would be lexicographically larger.
```

Example 2:
```
Input: nums = [1,2,1,2,1,2,1,2,1], k = 2
Output: [0,2,4]
```

Constraints:
* 1 <= nums.length <= 2 * 10^4
* 1 <= nums[i] <2^16
* 1 <= k <= floor(nums.length / 3)

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> maxSumOfThreeSubarrays(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> prefixSum(n+1, 0);
        
        for (int i = 1; i <= n; i++) {
            prefixSum[i] = prefixSum[i-1] + nums[i-1];
        }
        
        vector<int> left(n+1, 0);
        vector<int> leftInd(n+1, 0);
        vector<int> right(n+1, 0);
        vector<int> rightInd(n+1, 0);
        
        for (int i = k; i <= n; i++) {
            left[i] = max(left[i-1], prefixSum[i] - prefixSum[i-k]);
            if (left[i] == left[i-1]) 
                leftInd[i] = leftInd[i-1];
            else 
                leftInd[i] = i;
        }
        
        for (int i = n-k; i >= 0; i--) {
            right[i] = max(right[i+1], prefixSum[i+k] - prefixSum[i]);
            if (right[i] == prefixSum[i+k] - prefixSum[i]) 
                rightInd[i] = i;
            else
                rightInd[i] = rightInd[i+1];
        }
        
        int maxSum = 0, a, b, c;
        
        for (int i = k; i <= n - 2 * k; i++) {
            if (maxSum < left[i] + (prefixSum[i+k] - prefixSum[i]) + right[i+k]) {
                maxSum = left[i] + (prefixSum[i+k] - prefixSum[i]) + right[i+k];
                a = leftInd[i] - k;
                b = i;
                c = rightInd[i+k];
            }
        }
        
        return {a, b, c};
    }
};
```


