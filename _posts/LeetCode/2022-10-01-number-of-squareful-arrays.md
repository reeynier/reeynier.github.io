---
layout: post
title: "Number Of Squareful Arrays Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Dynamic Programming, Backtracking, Bit Manipulation ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 996. An array is squareful if the sum of every pair of adjacent elements is a perfect square.

---

<br />

## Description

LeetCode Problem 996.

An array is squareful if the sum of every pair of adjacent elements is a perfect square.

Given an integer array nums, return the number of permutations of nums that are squareful.

Two permutations perm1 and perm2 are different if there is some index i such that perm1[i] != perm2[i].

Example 1:
```
Input: nums = [1,17,8]
Output: 2
Explanation: [1,8,17] and [17,8,1] are the valid permutations.
```

Example 2:
```
Input: nums = [2,2,2]
Output: 1
```

Constraints:
* 1 <= nums.length <= 12
* 0 <= nums[i] <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    unordered_map<int, int> count;
    unordered_map<int, unordered_set<int>> cand;
    int res = 0;
    
    int numSquarefulPerms(vector<int>& A) {
        for (int &a : A) 
            count[a]++;
        for (auto &i : count) {
            for (auto &j : count) {
                int x = i.first, y = j.first, s = sqrt(x + y);
                if (s * s == x + y)
                    cand[x].insert(y);
            }
        }
        for (auto e : count)
            dfs(e.first, A.size() - 1);
        return res;
    }

    void dfs(int x, int left) {
        count[x]--;
        if (!left) 
            res++;
        for (int y : cand[x])
            if (count[y] > 0)
                dfs(y, left - 1);
        count[x]++;
    }
};
```


