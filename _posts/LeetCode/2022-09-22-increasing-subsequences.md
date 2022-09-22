---
layout: post
title: "Increasing Subsequences Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Backtracking, Bit Manipulation ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 491. Given an integer array nums, return all the different possible increasing subsequences of the given array with at least two elements. You may return the answer in any order.

---

<br />

## Description

LeetCode Problem 491.

Given an integer array nums, return all the different possible increasing subsequences of the given array with at least two elements. You may return the answer in any order.

The given array may contain duplicates, and two equal integers should also be considered a special case of increasing sequence.

Example 1:
```
Input: nums = [4,6,7,7]
Output: [[4,6],[4,6,7],[4,6,7,7],[4,7],[4,7,7],[6,7],[6,7,7],[7,7]]
```

Example 2:
```
Input: nums = [4,4,3,2,1]
Output: [[4,4]]
```

Constraints:
* 1 <= nums.length <= 15
* -100 <= nums[i] <= 100

<br />

## Sample C++ Code using Backtracking


```c
class Solution {
public:
    vector<vector<int>> findSubsequences(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> seq;
        dfs(res, seq, nums, 0);
        return res;
    }
    
    void dfs(vector<vector<int>>& res, vector<int>& seq, vector<int>& nums, int pos) {
        if(seq.size() > 1) res.push_back(seq);
        unordered_set<int> hash;
        for(int i = pos; i < nums.size(); ++i) {
            if((seq.empty() || nums[i] >= seq.back()) && hash.find(nums[i]) == hash.end()) {
                seq.push_back(nums[i]);
                dfs(res, seq, nums, i + 1);
                seq.pop_back();
                hash.insert(nums[i]);
            }
        }
    }
};
```


