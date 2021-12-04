---
layout: post
title: "Rotate Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Two Pointers ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 189. Given an array, rotate the array to the right by k steps, where k is non-negative.

---

<br />

## Description

LeetCode Problem 189.

Given an array, rotate the array to the right by k steps, where k is non-negative.

Example 1:
```
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

Example 2:
```
Input: nums = [-1,-100,3,99], k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

Constraints:
* 1 <= nums.length <= 10^5
* -2^31 <= nums[i] <= 2^31 - 1
* 0 <= k <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        if (n == 0)
            return;
        k = k % n;
        int tmp;
        
        
        for (int i = 0; i < n-k; i ++) {
            nums.push_back(nums[i]);
        }
        nums.erase(nums.begin(), nums.begin()+n-k);
        
    }
};
```


