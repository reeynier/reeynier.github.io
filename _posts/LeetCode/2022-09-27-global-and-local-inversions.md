---
layout: post
title: "Global And Local Inversions Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 775. You are given an integer array nums of length n which represents a permutation of all the integers in the range [0, n - 1].

---

<br />

## Description

LeetCode Problem 775.

You are given an integer array nums of length n which represents a permutation of all the integers in the range [0, n - 1].

The number of global inversions is the number of the different pairs (i, j) where:
* 0 <= i < j < n
* nums[i] > nums[j]
The number of local inversions is the number of indices i where:
* 0 <= i < n - 1
* nums[i] > nums[i + 1]

Return true if the number of global inversions is equal to the number of local inversions.

Example 1:
```
Input: nums = [1,0,2]
Output: true
Explanation: There is 1 global inversion and 1 local inversion.
```

Example 2:
```
Input: nums = [1,2,0]
Output: false
Explanation: There are 2 global inversions and 1 local inversion.
```

Constraints:
* n == nums.length
* 1 <= n <= 10^5
* 0 <= nums[i] < n
* All the integers of nums are unique.
* nums is a permutation of all the numbers in the range [0, n - 1].

<br />

## Sample C++ Code

```c
class Solution {
public:
    // The original order should be [0, 1, 2, 3, 4...], the number i should be on the position i.
    // We just check the offset of each number, if the absolute value is larger than 1, 
    // means the number of global inversion must be bigger than local inversion, 
    // because a local inversion is a global inversion, but a global one may not be local.
    bool isIdealPermutation(vector<int>& A) {
        for (int i = 0; i < A.size(); ++i) {
                if (abs(A[i] - i) > 1) return false;
            }
        return true;
    }
};
```


