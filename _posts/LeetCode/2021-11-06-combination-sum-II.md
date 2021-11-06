---
layout: post
title:  "Combination Sum II Problem"
categories: [ Algorithm ]
tags: [ Array, Backtracking, Leetcode ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 40. Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.
---

<br />

## Description

LeetCode Problem 40. 

Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.

Each number in candidates may only be used once in the combination.

Note: The solution set must not contain duplicate combinations.

 

Example 1:
```
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

Example 2:
```
Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
]
```

Constraints:

* 1 <= candidates.length <= 100
* 1 <= candidates[i] <= 50
* 1 <= target <= 30


<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<vector<int>> ans;
    
    void dfs(vector<int>& candidates, vector<int>& comb, int target, int idx) {
        if (target == 0)
            ans.push_back(comb);
        if (target <= 0)
            return;
        
        for (int i = idx; i < candidates.size(); i ++) {
            if (i > idx && candidates[i] == candidates[i-1])
                continue;
            if (target >= candidates[i]) {
                comb.push_back(candidates[i]);
                dfs(candidates, comb, target-candidates[i], i+1);
                comb.pop_back();
            }
        }
        return;
    }
    
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        vector<int> comb;
        sort(candidates.begin(), candidates.end());
        dfs(candidates, comb, target, 0);
        return ans;
    }
};
```
