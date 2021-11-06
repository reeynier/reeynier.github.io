---
layout: post
title:  "Permutations II Problem"
categories: [ Algorithm ]
tags: [ Array, Backtracking, Leetcode ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 47. Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.
---

<br />

## Description

LeetCode Problem 47. 

Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.

 

Example 1:
```
Input: nums = [1,1,2]
Output:
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```

Example 2:
```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

Constraints:

* 1 <= nums.length <= 8
* -10 <= nums[i] <= 10



<br />

## Sample C++ Code


```c
class Solution {
public:
    int n;
    vector<vector<int>> ans;
    set<vector<int>> visited;
    
    void backtrack(int idx, vector<int>& nums) {
        if (idx == n)
            visited.insert(nums);
        
        int tmp;
        for (int i = idx; i < n; i ++) {
            if (nums[idx] == nums[i] && i != idx)
                continue;
            
            tmp = nums[idx];
            nums[idx] = nums[i];
            nums[i] = tmp;
            
            backtrack(idx+1, nums);
            
            tmp = nums[idx];
            nums[idx] = nums[i];
            nums[i] = tmp;
        }
    }
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        n = nums.size();
        
        backtrack(0, nums);
        
        for (auto x : visited)
            ans.push_back(x);
        return ans;
    }
};
```
