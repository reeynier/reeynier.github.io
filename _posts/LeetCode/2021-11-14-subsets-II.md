---
layout: post
title:  "Subsets II Problem"
categories: [ Algorithm ]
tags: [ Array, Backtracking, Bit Manipulation, Leetcode ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 90. Given an integer array nums that may contain duplicates, return all possible subsets (the power set).
---

<br />

## Description

LeetCode Problem 90. 

Given an integer array nums that may contain duplicates, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

 

Example 1:
```
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

Example 2:
```
Input: nums = [0]
Output: [[],[0]]
```

Constraints:

* 1 <= nums.length <= 10
* -10 <= nums[i] <= 10

<br />

## Sample C++ Code


```c
class Solution {
public:
    
    int n;
    set<vector<int>> set_ans;
    
    void dfs(int idx, vector<int>& state, vector<int>& nums) {
        if (idx == n) {
            vector<int> s;
            for (int i = 0; i < n; i ++) {
                if (state[i] == 1)
                    s.push_back(nums[i]);
            }
            sort(s.begin(), s.end());
            set_ans.insert(s);
            return;
        }
        
        state[idx] = 0;
        dfs(idx+1, state, nums);
        
        state[idx] = 1;
        dfs(idx+1, state, nums);
    }
    
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        n = nums.size();
        vector<int> state(n, 0);
        
        dfs(0, state, nums);
        vector<vector<int>> ans;
        
        for (auto x : set_ans)
            ans.push_back(x);
        
        return ans;
    }
};
```
