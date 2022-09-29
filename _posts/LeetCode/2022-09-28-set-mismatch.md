---
layout: post
title: "Set Mismatch Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Bit Manipulation, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 645. You have a set of integers s, which originally contains all the numbers from 1 to n. Unfortunately, due to some error, one of the numbers in s got duplicated to another number in the set, which results in repetition of one number and loss of another number.

---

<br />

## Description

LeetCode Problem 645.

You have a set of integers s, which originally contains all the numbers from 1 to n. Unfortunately, due to some error, one of the numbers in s got duplicated to another number in the set, which results in repetition of one number and loss of another number.

You are given an integer array nums representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return them in the form of an array.

Example 1:
```
Input: nums = [1,2,2,4]
Output: [2,3]
```

Example 2:
```
Input: nums = [1,1]
Output: [1,2]
```

Constraints:
* 2 <= nums.length <= 10^4
* 1 <= nums[i] <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> findErrorNums(vector<int>& nums) {
        sort(begin(nums), end(nums));
        int dupl = -1;
        for (int i = 0; i < nums.size() - 1; i++) {
            if (nums[i] == nums[i + 1]) {
                dupl = nums[i];
                break;
            }
        }
        int sum = (nums.size() + 1) * nums.size() / 2;
        for (int i = 0; i < nums.size(); i++) {
            sum -= nums[i];
        }
        return { dupl, sum + dupl };
    }
};
```


