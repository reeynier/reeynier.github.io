---
layout: post
title: "Majority Element II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Sorting, Counting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 229. Given an integer array of size n, find all elements that appear more than &lfloor; n/3 &rfloor; times.

---

<br />

## Description

LeetCode Problem 229.

Given an integer array of size n, find all elements that appear more than &lfloor; n/3 &rfloor; times.

Example 1:
```
Input: nums = [3,2,3]
Output: [3]
```

Example 2:
```
Input: nums = [1]
Output: [1]
```

Example 3:
```
Input: nums = [1,2]
Output: [1,2]
```

Constraints:
* 1 <= nums.length <= 5 * 10^4
* -10^9 <= nums[i] <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int s = nums.size();
        
        map<int, int> counter;
        for(int i = 0; i < s; i++)
        {
            counter[nums[i]]++;
        }
        
        vector<int> result;
        for(auto i : counter)
        {
            if(i.second > s / 3)
            {
                result.push_back(i.first);
            }
        }
        
        return result;
    }
};
```


