---
layout: post
title: "Partition Equal Subset Sum Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 416. Given a non-empty array nums containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

---

<br />

## Description

LeetCode Problem 416.

Given a non-empty array nums containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

Example 1:
```
Input: nums = [1,5,11,5]
Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

Example 2:
```
Input: nums = [1,2,3,5]
Output: false
Explanation: The array cannot be partitioned into equal sum subsets.
```

Constraints:
* 1 <= nums.length <= 200
* 1 <= nums[i] <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool checkPar(vector<int>& nums, int target, int len) {
        if (target == 0)
            return true;
        if ((target != 0) && (len == 0))
            return false;
        if (nums[len-1] > target)
            return false;
        return checkPar(nums, target-nums[len-1], len-1) || 
            checkPar(nums, target, len-1);
    }
    
    bool canPartition(vector<int>& nums) {
        int len = nums.size();
        
        int target = 0;
        for (int i = 0; i < len; i ++) {
            target += nums[i];
        }
        if (target % 2 != 0)
            return false;
        
        return checkPar(nums, target / 2, len);
    }
};
```


