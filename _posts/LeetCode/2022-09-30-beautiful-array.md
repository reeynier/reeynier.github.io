---
layout: post
title: "Beautiful Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Divide and Conquer ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 932. Given the integer n, return any beautiful array nums of length n. There will be at least one valid answer for the given n.

---

<br />

## Description

LeetCode Problem 932.

An array nums of length n is beautiful if:
* nums is a permutation of the integers in the range [1, n].
* For every 0 <= i < j < n, there is no index k with i < k < j where 2 * nums[k] == nums[i] + nums[j].

Given the integer n, return any beautiful array nums of length n. There will be at least one valid answer for the given n.

Example 1:
```
Input: n = 4
Output: [2,1,4,3]
```

Example 2:
```
Input: n = 5
Output: [3,1,2,5,4]
```

Constraints:
* 1 <= n <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> beautifulArray(int N) {
        if (N == 1) return {1};
        vector<int> even = beautifulArray(N / 2);
        vector<int> odd = beautifulArray(N - N / 2);
        vector<int> rtn;
        for (int x : even) 
            rtn.push_back(x * 2);
        for (int x : odd) 
            rtn.push_back(x * 2 - 1);
        return rtn;
    }
};
```


