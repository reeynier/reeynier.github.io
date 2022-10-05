---
layout: post
title: "Sum Of Subsequence Widths Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Sorting ]
similar: [ Sorting ]
featured: false
hidden: false
excerpt: LeetCode 891. The width of a sequence is the difference between the maximum and minimum elements in the sequence.

---

<br />

## Description

LeetCode Problem 891.

The width of a sequence is the difference between the maximum and minimum elements in the sequence.

Given an array of integers nums, return the sum of the widths of all the non-empty subsequences of nums. Since the answer may be very large, return it modulo 10^9 + 7.

A subsequence is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, [3,6,2,7] is a subsequence of the array [0,3,1,6,2,2,7].

Example 1:
```
Input: nums = [2,1,3]
Output: 6
Explanation: The subsequences are [1], [2], [3], [2,1], [2,3], [1,3], [2,1,3].
The corresponding widths are 0, 0, 0, 1, 1, 2, 2.
The sum of these widths is 6.
```

Example 2:
```
Input: nums = [2]
Output: 0
```

Constraints:
* 1 <= nums.length <= 10^5
* 1 <= nums[i] <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    int sumSubseqWidths(vector<int>& arr) {
        sort(arr.begin(), arr.end());
        long power = 1, res = 0, mod = 1e9 + 7, n = arr.size();
        
        // adding maximums
        // number of times this item will be maximum
        for (int i = 0; i < n; i++) {
            res = (res + arr[i] * power) % mod;
            power = (power * 2) % mod;
        }
        
        // subtracting minimums
        // number of times this item will be minimum
        power = 1;
        for (int i = n-1; i >= 0; i--) {
            res = (res - arr[i] * power + mod) % mod;
            power = (power * 2) % mod;
        }
        return (res + mod) % mod;
    }
};
```


