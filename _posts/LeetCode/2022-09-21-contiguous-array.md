---
layout: post
title: "Contiguous Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Prefix Sum ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 525. Given a binary array nums, return the maximum length of a contiguous subarray with an equal number of 0 and 1.

---

<br />

## Description

LeetCode Problem 525.

Given a binary array nums, return the maximum length of a contiguous subarray with an equal number of 0 and 1.

Example 1:
```
Input: nums = [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with an equal number of 0 and 1.
```

Example 2:
```
Input: nums = [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

Constraints:
* 1 <= nums.length <= 10^5
* nums[i] is either 0 or 1.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findMaxLength(vector<int>& nums) {
        int sum = 0, maxLen = 0;
        unordered_map<int, int> seen{ {0, -1} };
        
        for(int i = 0; i < nums.size(); i++) {
            sum += nums[i]==1 ? 1 : -1;
            if(seen.count(sum)) 
                maxLen = max(maxLen, i-seen[sum]);
            else 
                seen[sum] = i;
        }
        return maxLen;
    }
};
```


