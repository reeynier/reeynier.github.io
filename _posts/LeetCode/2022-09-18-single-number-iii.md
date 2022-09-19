---
layout: post
title: "Single Number III Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Bit Manipulation ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 260. Given an integer array nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once. You can return the answer in any order.

---

<br />

## Description

LeetCode Problem 260.

Given an integer array nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once. You can return the answer in any order.

You must write analgorithm that runs in linear runtime complexity and usesonly constant extra space.

Example 1:
```
Input: nums = [1,2,1,3,2,5]
Output: [3,5]
Explanation:  [5, 3] is also a valid answer.
```

Example 2:
```
Input: nums = [-1,0]
Output: [-1,0]
```

Example 3:
```
Input: nums = [0,1]
Output: [1,0]
```

Constraints:
* 2 <= nums.length <= 3 * 10^4
* -2^31 <= nums[i] <= 2^31 - 1
* Each integer in nums will appear twice, only two integers will appear once.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> singleNumber(vector<int> &nums) {
        unordered_map<int, int> freq;

        for (auto &num: nums) ++freq[num];
        
        vector<int> ans;

        for (auto &[x, f]: freq)
            if (f == 1) {
                ans.push_back(x);
                if (ans.size() == 2)
                    return ans;
            }
        return ans;
    }
};
```


