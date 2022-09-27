---
layout: post
title: "Partition To K Equal Sum Subsets Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Backtracking, Bit Manipulation, Memoization, Bitmask ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 698. Given an integer array nums and an integer k, return true if it is possible to divide this array into k non-empty subsets whose sums are all equal.

---

<br />

## Description

LeetCode Problem 698.

Given an integer array nums and an integer k, return true if it is possible to divide this array into k non-empty subsets whose sums are all equal.

Example 1:
```
Input: nums = [4,3,2,3,5,2,1], k = 4
Output: true
Explanation: It's possible to divide it into 4 subsets (5), (1, 4), (2,3), (2,3) with equal sums.
```

Example 2:
```
Input: nums = [1,2,3,4], k = 3
Output: false
```

Constraints:
* 1 <= k <= nums.length <= 16
* 1 <= nums[i] <= 10^4
* The frequency of each element is in the range [1, 4].

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool checkPar(vector<int>& nums, vector<int>& visited, 
                  int target, int curr_sum, int idx, int k) {
        if (k == 1)
            return true;
        if (curr_sum == target)
            return checkPar(nums, visited, target, 0, 0, k-1);
        for (int i = idx; i < nums.size(); i ++) {
            if ((visited[i] == 0) && (curr_sum+nums[i]<=target)) {
                visited[i] = 1;
                if (checkPar(nums, visited, target, curr_sum+nums[i], i+1, k))
                    return true;
                visited[i] = 0;
            }
        }
        return false;
    }
    bool canPartitionKSubsets(vector<int>& nums, int k) {
        int len = nums.size();
        int target = 0;
        vector<int> visited(len, 0);
        for (int i = 0; i < len; i ++)
            target += nums[i];
        if (target % k != 0)
            return false;
        
        return checkPar(nums, visited, target/k, 0, 0, k);
    }
};
```


