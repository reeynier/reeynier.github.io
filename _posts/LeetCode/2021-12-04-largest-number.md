---
layout: post
title: "Largest Number Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Greedy, Sorting ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 179. Given a list of non-negative integers nums, arrange them such that they form the largest number.

---

<br />

## Description

LeetCode Problem 179.

Given a list of non-negative integers nums, arrange them such that they form the largest number.
Note: The result may be very large, so you need to return a string instead of an integer.

Example 1:
```
Input: nums = [10,2]
Output: "210"
```

Example 2:
```
Input: nums = [3,30,34,5,9]
Output: "9534330"
```

Example 3:
```
Input: nums = [1]
Output: "1"
```

Example 4:
```
Input: nums = [10]
Output: "10"
```

Constraints:
* 1 <= nums.length <= 100
* 0 <= nums[i] <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
    struct comp {
        bool operator() (int a, int b) {
            string comb1 = to_string(a) + to_string(b);
            string comb2 = to_string(b) + to_string(a);
            return comb1 > comb2;
        }
    } mycomp;
public:
    string largestNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end(), mycomp);
        if (nums[0] == 0) return "0";
        string res = "";
        for (auto num : nums) {
            res = res + to_string(num);
        }
        return res;
    }
};
```


