---
layout: post
title: "Majority Element Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Divide and Conquer, Sorting, Counting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 169. Given an array nums of size n, return the majority element.

---

<br />

## Description

LeetCode Problem 169.

Given an array nums of size n, return the majority element.

The majority element is the element that appears more than [n / 2]; times. You may assume that the majority element always exists in the array.

Example 1:
```
Input: nums = [3,2,3]
Output: 3
```

Example 2:
```
Input: nums = [2,2,1,1,1,2,2]
Output: 2
```

Constraints:
* n == nums.length
* 1 <= n <= 5 * 10^4
* -2^31 <= nums[i] <= 2^31 - 1
Follow-up: Could you solve the problem in linear time and in O(1) space?
<br />

## Sample C++ Code


```c
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        unordered_map<int, int> ht;
        unordered_map<int, int>::iterator it;
        for (int i = 0; i < nums.size(); i ++) {
            if (ht.find(nums[i]) == ht.end())
                ht[nums[i]] = 0;
            ht[nums[i]] ++;
            if (ht[nums[i]] > nums.size() / 2)
                return nums[i];
        }
        return 0;
    }
};
```


