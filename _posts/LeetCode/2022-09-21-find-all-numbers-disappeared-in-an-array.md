---
layout: post
title: "Find All Numbers Disappeared In An Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 448. Given an array nums of n integers where nums[i] is in the range [1, n], return an array of all the integers in the range [1, n] that do not appear in nums.

---

<br />

## Description

LeetCode Problem 448.

Given an array nums of n integers where nums[i] is in the range [1, n], return an array of all the integers in the range [1, n] that do not appear in nums.

Example 1:
```
Input: nums = [4,3,2,7,8,2,3,1]
Output: [5,6]
```

Example 2:
```
Input: nums = [1,1]
Output: [2]
```

Constraints:
* n == nums.length
* 1 <= n <= 10^5
* 1 <= nums[i] <= n

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        vector<int> ans;
        
        for (int i = 0; i < nums.size(); i ++) {
            int nxt = nums[i] - 1;
            while (nums[nxt] != nxt + 1) {
                int nxt_nxt = nums[nxt] - 1;
                nums[nxt] = nxt + 1;
                nxt = nxt_nxt;
            }
        }
        
        for (int i = 0; i < nums.size(); i ++) {
            if (nums[i] != i + 1)
                ans.push_back(i + 1);
        }

        return ans;
    }
};
```


