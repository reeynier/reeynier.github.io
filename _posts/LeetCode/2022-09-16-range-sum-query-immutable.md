---
layout: post
title: "Range Sum Query - Immutable Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Design, Prefix Sum ]
similar: [ Design ]
featured: false
hidden: false
excerpt: LeetCode 303. Given an integer array nums, handle multiple queries of the following type

---

<br />

## Description

LeetCode Problem 303.

Given an integer array nums, handle multiple queries of the following type:
* Calculate the sum of the elements of nums between indices left and right inclusive where left <= right.
Implement the NumArray class:
* NumArray(int[] nums) Initializes the object with the integer array nums.
* int sumRange(int left, int right) Returns the sum of the elements of nums between indices left and right inclusive (i.e. nums[left] + nums[left + 1] + ... + nums[right]).

Example 1:
```
Input
["NumArray", "sumRange", "sumRange", "sumRange"]
[[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]
Output
[null, 1, -1, -3]
Explanation
NumArray numArray = new NumArray([-2, 0, 3, -5, 2, -1]);
numArray.sumRange(0, 2); // return (-2) + 0 + 3 = 1
numArray.sumRange(2, 5); // return 3 + (-5) + 2 + (-1) = -1
numArray.sumRange(0, 5); // return (-2) + 0 + 3 + (-5) + 2 + (-1) = -3
```

Constraints:
* 1 <= nums.length <= 10^4
* -10^5 <= nums[i] <= 10^5
* 0 <= left <= right < nums.length
* At most 10^4 calls will be made to sumRange.

<br />

## Sample C++ Code


```c
class NumArray {
public:
    vector<int> dp;
    
    NumArray(vector<int>& nums) {
        if (nums.size() == 0)
            return;
        dp.push_back(nums[0]);
        for (int i = 1; i < nums.size(); i ++) {
            dp.push_back(dp[i-1] + nums[i]);
        }    
    }
    
    int sumRange(int i, int j) {
        if (i == 0)
            return dp[j];
        else
            return (dp[j]-dp[i-1]);
    }
};

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray* obj = new NumArray(nums);
 * int param_1 = obj->sumRange(i,j);
 */
```


