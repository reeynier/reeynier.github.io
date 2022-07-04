---
layout: post
title: "Contains Duplicate Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 217. Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

---

<br />

## Description

LeetCode Problem 217.

Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

Example 1:
```
Input: nums = [1,2,3,1]
Output: true
```

Example 2:
```
Input: nums = [1,2,3,4]
Output: false
```

Example 3:
```
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```

Constraints:
* 1 <= nums.length <= 10^5
* -10^9 <= nums[i] <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        bool distinct = true;
        map<int, int> ht;
        for (int i = 0; i < nums.size(); i ++) {
            int n = nums[i];
            if (ht.find(n) == ht.end())
                ht[n] = 0;
            ht[n] ++;
            if (ht[n] > 1) {
                distinct = false;
            }
        }
        return !distinct;          
    }
};
```


