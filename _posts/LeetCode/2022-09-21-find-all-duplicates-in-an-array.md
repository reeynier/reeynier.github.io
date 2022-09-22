---
layout: post
title: "Find All Duplicates In An Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 442. Given an integer array nums of length n where all the integers of nums are in the range [1, n] and each integer appears once or twice, return an array of all the integers that appears twice.

---

<br />

## Description

LeetCode Problem 442.

Given an integer array nums of length n where all the integers of nums are in the range [1, n] and each integer appears once or twice, return an array of all the integers that appears twice.

You must write an algorithm that runs inO(n)time and uses only constant extra space.

Example 1:
```
Input: nums = [4,3,2,7,8,2,3,1]
Output: [2,3]
```

Example 2:
```
Input: nums = [1,1,2]
Output: [1]
```

Example 3:
```
Input: nums = [1]
Output: []
```

Constraints:
* n == nums.length
* 1 <= n <= 10^5
* 1 <= nums[i] <= n
* Each element in nums appears once or twice.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        vector<int> ans;
        for (int i = 0; i < nums.size(); i ++) {
            int x = abs(nums[i]);
            if (nums[x-1] > 0) {
                nums[x-1] = -nums[x-1];
            } else {
                ans.push_back(x);
            }
        }
        return ans;
    }
};
```


