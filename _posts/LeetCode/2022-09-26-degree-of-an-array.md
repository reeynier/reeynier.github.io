---
layout: post
title: "Degree Of An Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 697. Given a non-empty array of non-negative integers nums, the degree of this array is defined as the maximum frequency of any one of its elements.

---

<br />

## Description

LeetCode Problem 697.

Given a non-empty array of non-negative integers nums, the degree of this array is defined as the maximum frequency of any one of its elements.

Your task is to find the smallest possible length of a (contiguous) subarray of nums, that has the same degree as nums.

Example 1:
```
Input: nums = [1,2,2,3,1]
Output: 2
Explanation: 
The input array has a degree of 2 because both elements 1 and 2 appear twice.
Of the subarrays that have the same degree:
[1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]
The shortest length is 2. So return 2.
```

Example 2:
```
Input: nums = [1,2,2,3,1,4,2]
Output: 6
Explanation: 
The degree is 3 because the element 2 is repeated 3 times.
So [2,2,3,1,4,2] is the shortest subarray, therefore returning 6.
```

Constraints:
* nums.length will be between 1 and 50,000.
* nums[i] will be an integer between 0 and 49,999.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findShortestSubArray(vector<int>& nums) {
        unordered_map<int,vector<int>> mp;
        for (int i = 0; i < nums.size(); i++) 
            mp[nums[i]].push_back(i);
        int degree=0;
        for (auto it = mp.begin(); it != mp.end(); it++) 
            degree = max(degree, int(it->second.size()));
        int shortest = nums.size();
        for (auto it = mp.begin(); it != mp.end(); it++) {
            if (it->second.size() == degree) {
                shortest = min(shortest, it->second.back()-it->second[0] + 1);
            }
        }
        return shortest;
    }
};
```


