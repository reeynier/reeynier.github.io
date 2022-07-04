---
layout: post
title: "Contains Duplicate II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Sliding Window ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 219. Given an integer array nums and an integer k, return true if there are two distinct indices i and j in the array such that nums[i] == nums[j] and abs(i - j) <= k.

---

<br />

## Description

LeetCode Problem 219.

Given an integer array nums and an integer k, return true if there are two distinct indices i and j in the array such that nums[i] == nums[j] and abs(i - j) <= k.

Example 1:
```
Input: nums = [1,2,3,1], k = 3
Output: true
```

Example 2:
```
Input: nums = [1,0,1,1], k = 1
Output: true
```

Example 3:
```
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```

Constraints:
* 1 <= nums.length <= 10^5
* -10^9 <= nums[i] <= 10^9
* 0 <= k <= 10^5

<br />

## Sample C++ Code


```c
bool containsNearbyDuplicate(vector<int>& nums, int k) {
    unordered_map<int,int> nmap;
    for (int i = 0; i <nums.size();i++) {
        if (nmap.count(nums[i]) == 0)
            nmap[nums[i]] = i;
        else if (i - nmap[nums[i]] <=k)
            return true;
        else
            nmap[nums[i]] = i;
    }
    return false;
}
```


