---
layout: post
title: "Smallest Range II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Greedy, Sorting ]
similar: [ Sorting ]
featured: false
hidden: false
excerpt: LeetCode 910. You are given an integer array nums and an integer k.

---

<br />

## Description

LeetCode Problem 910.

You are given an integer array nums and an integer k.

For each index i where 0 <= i < nums.length, change nums[i] to be either nums[i] + k or nums[i] - k.

The score of nums is the difference between the maximum and minimum elements in nums.

Return the minimum score of nums after changing the values at each index.

Example 1:
```
Input: nums = [1], k = 0
Output: 0
Explanation: The score is max(nums) - min(nums) = 1 - 1 = 0.
```

Example 2:
```
Input: nums = [0,10], k = 2
Output: 6
Explanation: Change nums to be [2, 8]. The score is max(nums) - min(nums) = 8 - 2 = 6.
```

Example 3:
```
Input: nums = [1,3,6], k = 3
Output: 3
Explanation: Change nums to be [4, 6, 3]. The score is max(nums) - min(nums) = 6 - 3 = 3.
```

Constraints:
* 1 <= nums.length <= 10^4
* 0 <= nums[i] <= 10^4
* 0 <= k <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int smallestRangeII(vector<int>& A, int K) {
        sort(A.begin(), A.end());
        int res = A[A.size() - 1] - A[0];
        int left = A[0] + K, right = A[A.size() - 1] - K;
        for (int i = 0; i < A.size() - 1; i++) {
            int maxi = max(A[i] + K, right);
            int mini = min(left, A[i + 1] - K);
            res = min(res, maxi - mini);
        }
        return res;
    }
};
```


