---
layout: post
title:  "Combinations Problem"
categories: [ Data Structure ]
tags: [ Array, Backtracking, Leetcode ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 77. Given two integers n and k, return all possible combinations of k numbers out of the range [1, n].
---

<br />

## Description

LeetCode Problem 77. 

Given two integers n and k, return all possible combinations of k numbers out of the range [1, n].

You may return the answer in any order.

 

Example 1:
```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

Example 2:
```
Input: n = 1, k = 1
Output: [[1]]
```
 

Constraints:

* 1 <= n <= 20
* 1 <= k <= n

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
            comb.push_back(candidates[i]);
            dfs(candidates, comb, target-1, i+1);
            comb.pop_back();
        }
    }
    
    vector<vector<int>> combine(int n, int k) {
        vector<int> candidates;
        for (int i = 1; i <= n; i ++) candidates.push_back(i);
        vector<int> comb;
        
        dfs(candidates, comb, k, 0);
        
        return ans;
    }
};
```
