---
layout: post
title:  "Sum Of Unique Elements Problem"
categories: [ Data Structure ]
tags: [ Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 1748. You are given an integer array nums. The unique elements of an array are the elements that appear exactly once in the array.
---

<br />

## Description

LeetCode Problem 1748. 

You are given an integer array nums. The unique elements of an array are the elements that appear exactly once in the array.

Return the sum of all the unique elements of nums.

 

Example 1:
```
Input: nums = [1,2,3,2]
Output: 4
Explanation: The unique elements are [1,3], and the sum is 4.
```

Example 2:
```
Input: nums = [1,1,1,1,1]
Output: 0
Explanation: There are no unique elements, and the sum is 0.
```

Example 3:
```
Input: nums = [1,2,3,4,5]
Output: 15
Explanation: The unique elements are [1,2,3,4,5], and the sum is 15.
```

<br />

## Solution

We can use a hash table to count the frequency of each number. We then scan through the hash table, and add up the numbers that has the frequency of 1. The time complexity is O(n), and the space complexity is O(n).

<br />

## Sample C++ Code


This is a C++ solution using a `hash table`.

```c
class Solution {
public:
    int sumOfUnique(vector<int>& nums) {
        unordered_map<int, int> map;
        unordered_map<int, int>::iterator it;
        
        int count = 0;
        
        for (int i:nums) {
            map[i]++;
        }
        
        for (it = map.begin(); it != map.end(); it++) {
            if (it->second == 1) {
                count += it->first;
            }
        }
        
        return count;
    }
};
```
