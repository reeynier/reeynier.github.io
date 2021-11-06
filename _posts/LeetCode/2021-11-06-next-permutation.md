---
layout: post
title:  "Next Permutation Problem"
categories: [ Data Structure ]
tags: [ Array, Two Pointers, Leetcode ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 31. Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.
---

<br />

## Description

LeetCode Problem 31. 

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such an arrangement is not possible, it must rearrange it as the lowest possible order (i.e., sorted in ascending order).

The replacement must be in place and use only constant extra memory.

 

Example 1:
```
Input: nums = [1,2,3]
Output: [1,3,2]
```

Example 2:
```
Input: nums = [3,2,1]
Output: [1,2,3]
```

Example 3:
```
Input: nums = [1,1,5]
Output: [1,5,1]
```

Example 4:
```
Input: nums = [1]
Output: [1]
```

Constraints:

* 1 <= nums.length <= 100
* 0 <= nums[i] <= 100



<br />

## Sample C++ Code


```c
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();
        int i = n-2, tmp, j, k;
        
        while (i >= 0 && nums[i] >= nums[i+1]) i --;
        
        if (i >= 0) {
            k = n-1;
            while (k > i && nums[k] <= nums[i]) k --;
            tmp = nums[k];
            nums[k] = nums[i];
            nums[i] = tmp;
        }
        
        j = i+1, k = n-1;
        while (j < k) {
            tmp = nums[j];
            nums[j] = nums[k];
            nums[k] = tmp;
            j ++;
            k --;
        }
        return;
    }
};
```
