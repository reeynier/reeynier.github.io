---
layout: post
title: "Single Number II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Bit Manipulation ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 137. Given an integer array nums whereevery element appears three times except for one, which appears exactly once. Find the single element and return it.

---

<br />

## Description

LeetCode Problem 137.

Given an integer array nums whereevery element appears three times except for one, which appears exactly once. Find the single element and return it.

You mustimplement a solution with a linear runtime complexity and useonly constantextra space.

Example 1:
```
Input: nums = [2,2,3,2]
Output: 3
```

Example 2:
```
Input: nums = [0,1,0,1,0,1,99]
Output: 99
```

Constraints:
* 1 <= nums.length <= 3 * 10^4
* -2^31 <= nums[i] <= 2^31 - 1
* Each element in nums appears exactly three times except for one element which appears once.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int n = nums.size();
        long ans;
        int x, t;
        ans = 0;
        int p = 0;
		// We have 32 bits integers as input
        for(int i = 0; i < 32; i++) {
            t = 0;
            //calculate sum of ith bit for all numbers in nums
            for(int j = 0; j < n;j++) {
                x = nums[j] & 1;
                t = t + x;
                nums[j] = nums[j] >> 1;
            }
            t = t % 3;
            //the bit that does not occur as multiple of 3 is left as a remainder 
            ans = ans + t * pow(2, p);
            p++;
        }
        return ans;
    }
};
```


