---
layout: post
title: "Sort Array By Parity Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Two Pointers, Sorting ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 905. Given an integer array nums, move all the even integers at the beginning of the array followed by all the odd integers.

---

<br />

## Description

LeetCode Problem 905.

Given an integer array nums, move all the even integers at the beginning of the array followed by all the odd integers.

Return any array that satisfies this condition.

Example 1:
```
Input: nums = [3,1,2,4]
Output: [2,4,3,1]
Explanation: The outputs [4,2,3,1], [2,4,1,3], and [4,2,1,3] would also be accepted.
```

Example 2:
```
Input: nums = [0]
Output: [0]
```

Constraints:
* 1 <= nums.length <= 5000
* 0 <= nums[i] <= 5000

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> sortArrayByParity(vector<int>& A) {
        int j = 0;
        for (int i = 0; i < A.size(); i++) {
            if (A[i] % 2 == 0) {
                swap(A[i], A[j]);
                j ++;
            }
        }
        return A;
    }
};
```


