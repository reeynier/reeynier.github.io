---
layout: post
title:  "First Missing Positive Problem"
categories: [ Algorithm ]
tags: [ Array, Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 41. Given an unsorted integer array nums, return the smallest missing positive integer.
---

<br />

## Description

LeetCode Problem 41. 

Given an unsorted integer array nums, return the smallest missing positive integer.

You must implement an algorithm that runs in O(n) time and uses constant extra space.

 

Example 1:
```
Input: nums = [1,2,0]
Output: 3
```

Example 2:
```
Input: nums = [3,4,-1,1]
Output: 2
```

Example 3:
```
Input: nums = [7,8,9,11,12]
Output: 1
```

Constraints:

* 1 <= nums.length <= 5 * 10^5
* -2^31 <= nums[i] <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int len = nums.size();
        
        for (int i = 0; i < len; i ++) {
            if (nums[i] < 0 || nums[i] > len || nums[i] == i+1) 
                continue;
            int nxt = nums[i] - 1;
            while (nxt >= 0 && nxt < len && nums[nxt] != nxt+1) {
                int nxt_nxt = nums[nxt] - 1;
                nums[nxt] = nxt + 1;
                nxt = nxt_nxt;
            }
        }
        
        for (int i = 0; i < len; i ++) {
            if (nums[i] != i + 1)
                return i + 1;
        }
        return len + 1;
    }
};
```
