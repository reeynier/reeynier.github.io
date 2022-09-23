---
layout: post
title: "Minimum Moves To Equal Array Elements Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 453. Given an integer array nums of size n, return the minimum number of moves required to make all array elements equal.

---

<br />

## Description

LeetCode Problem 453.

Given an integer array nums of size n, return the minimum number of moves required to make all array elements equal.

In one move, you can increment n - 1 elements of the array by 1.

Example 1:
```
Input: nums = [1,2,3]
Output: 3
Explanation: Only three moves are needed (remember each move increments two elements):
[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```

Example 2:
```
Input: nums = [1,1,1]
Output: 0
```

Constraints:
* n == nums.length
* 1 <= nums.length <= 10^5
* -10^9 <= nums[i] <= 10^9
* The answer is guaranteed to fit in a 32-bit integer.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int minMoves(vector<int>& nums) {
        int m = INT_MAX;
        for (int n : nums) m = min(m, n);
        int ans = 0;
        for (int n : nums) ans += n - m;
        return ans;
    }
};
```


