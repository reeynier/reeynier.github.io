---
layout: post
title:  "Permutations Problem"
categories: [ Algorithm ]
tags: [ Array, Backtracking, Leetcode ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 46. Given an array nums of distinct integers, return all the possible permutations.
---

<br />

## Description

LeetCode Problem 46. 

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

 

Example 1:
```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

Example 2:
```
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```

Example 3:
```
Input: nums = [1]
Output: [[1]]
```
 

Constraints:

* 1 <= nums.length <= 6
* -10 <= nums[i] <= 10
* All the integers of nums are unique.


<br />

## Sample C++ Code


```c
class Solution {
public:
    int n;
    vector<vector<int>> ans;
    
    void backtrack(int idx, vector<int>& nums) {
        if (idx == n) 
            ans.push_back(nums);
        
        int tmp;
        for (int i = idx; i < n; i ++) {
            tmp = nums[i];
            nums[i] = nums[idx];
            nums[idx] = tmp;
            
            backtrack(idx + 1, nums);
            
            tmp = nums[i];
            nums[i] = nums[idx];
            nums[idx] = tmp;
        }
    }
    
    vector<vector<int>> permute(vector<int>& nums) {
        n = nums.size();
        
        backtrack(0, nums);
        
        return ans;
    }
};
```
