---
layout: post
title: "Matchsticks To Square Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Backtracking, Bit Manipulation, Bitmask ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 473. You are given an integer array matchsticks where matchsticks[i] is the length of the i^th matchstick. You want to use all the matchsticks to make one square. You should not break any stick, but you can link them up, and each matchstick must be used exactly one time.

---

<br />

## Description

LeetCode Problem 473.

You are given an integer array matchsticks where matchsticks[i] is the length of the i^th matchstick. You want to use all the matchsticks to make one square. You should not break any stick, but you can link them up, and each matchstick must be used exactly one time.

Return true if you can make this square and false otherwise.

Example 1: 
```
Input: matchsticks = [1,1,2,2,2]
Output: true
Explanation: You can form a square with length 2, one side of the square came two sticks with length 1.
```

Example 2:
```
Input: matchsticks = [3,3,3,3,4]
Output: false
Explanation: You cannot find a way to form a square with all the matchsticks.
```

Constraints:
* 1 <= matchsticks.length <= 15
* 1 <= matchsticks[i] <= 10^8

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool dfs(vector<int>& nums, vector<int>& visited, 
               int curr_sum, int target, int k, int start) {
        if (k == 1)
            return true;
        if (curr_sum == target)
            return dfs(nums, visited, 0, target, k-1, 0);
        
        for (int i = start; i < nums.size(); i ++) {
            if (visited[i] == 0 && curr_sum + nums[i] <= target) {
                visited[i] = 1;
                if (dfs(nums, visited, curr_sum+nums[i], target, k, i))
                    return true;
                visited[i] = 0;
            }
        }
        return false;
    }
    
    bool makesquare(vector<int>& nums) {
        int l = nums.size();
        if (l == 0) return false;
        
        int sum = 0;
        for (int i = 0; i < nums.size(); i ++) 
            sum += nums[i];
        if (sum % 4 != 0)
            return false;
        vector<int> visited(l, 0);
        return dfs(nums, visited, 0, sum / 4, 4, 0);
    }
};
```


