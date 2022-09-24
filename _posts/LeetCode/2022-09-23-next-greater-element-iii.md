---
layout: post
title: "Next Greater Element III Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Two Pointers, String ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 556. Given a positive integer n, find the smallest integer which has exactly the same digits existing in the integer n and is greater in value than n. If no such positive integer exists, return -1.

---

<br />

## Description

LeetCode Problem 556.

Given a positive integer n, find the smallest integer which has exactly the same digits existing in the integer n and is greater in value than n. If no such positive integer exists, return -1.

Note that the returned integer should fit in 32-bit integer, if there is a valid answer but it does not fit in 32-bit integer, return -1.

Example 1:
```
Input: n = 12
Output: 21
```

Example 2:
```
Input: n = 21
Output: -1
```

Constraints:
* 1 <= n <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool nextPermutation(string& nums) {
        int i = nums.size()-1;
        while (i > 0 && nums[i-1] >= nums[i]) i--;
        if (i == 0) return false;
        
        int j = nums.size()-1;
        while (j > 0 && nums[j] <= nums[i-1]) j--;
        swap(nums[j], nums[i-1]);
        reverse(nums.begin()+i, nums.end());
        return true;
    }
    
    int nextGreaterElement(int n) {
        string num = to_string(n);
        bool res = nextPermutation(num);
        size_t ans = stoll(num);
        return (!res || ans > INT_MAX) ? -1 : ans;
    }
};
```


