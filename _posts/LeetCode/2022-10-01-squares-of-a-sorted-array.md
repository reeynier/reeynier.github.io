---
layout: post
title: "Squares Of A Sorted Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Two Pointers, Sorting ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 977. Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

---

<br />

## Description

LeetCode Problem 977.

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

Example 1:
```
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
```

Example 2:
```
Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]
```

Constraints:
* <span>1 <= nums.length <= </span>10^4
* -10^4 <= nums[i] <= 10^4
* nums is sorted in non-decreasing order.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> sortedSquares(vector<int>& A) {
        int len = A.size();
        int i = 0; 
        while ((i < len) && (A[i] < 0)) i ++;
        i --;
        int j = i + 1;
        vector<int> ans;
        int left, right;
        while ((i >= 0) && (j < len)) {
            left = A[i] * A[i];
            right = A[j] * A[j];
            if (left < right) {
                ans.push_back(left);
                i --;
            } else {
                ans.push_back(right);
                j ++;
            }
        }
        while (i >= 0) {
            ans.push_back(A[i]*A[i]);
            i --;
        }
        while (j < len) {
            ans.push_back(A[j]*A[j]);
            j ++;
        }
        return ans;
    }
};
```


