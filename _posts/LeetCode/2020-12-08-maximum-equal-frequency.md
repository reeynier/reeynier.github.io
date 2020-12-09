---
layout: post
title:  "Maximum Equal Frequency"
categories: [ Data Structure ]
tags: [ Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 1224. Given an array **nums** of positive integers, return the longest possible length of an array **prefix** of **nums**,
---

<br />

## Description

LeetCode Problem 1224. Given an array **nums** of positive integers, return the longest possible length of an array **prefix** of **nums**, such that it is possible to remove exactly one element from this prefix so that every number that has appeared in it will have the same number of occurrences.

If after removing one element there are no remaining elements, it is still considered that every appeared number has the same number of occurrences (0).




Example: 
```
Input: nums = [2,2,1,1,5,3,3,5]
Output: 7
Explanation: For the subarray [2,2,1,1,5,3,3] of length 7, if we remove nums[4]=5, we will get [2,2,1,1,3,3], so that each number will appear exactly twice.

Input: nums = [1,1,1,2,2,2,3,3,3,4,4,4,5]
Output: 13

Input: nums = [1,1,1,2,2,2]
Output: 5

Input: nums = [10,2,8,9,3,8,1,5,2,3,7,6]
Output: 8
```

<br />

## Solution


The basic idea to solve this problem is to enumerate all possible prefixes of the array, and check whether each prefix satisfy the requirement -- by removing exactly one element from the prefix, every number remaining in the prefix appear has the same number of occurrences.

To enumerate every possible prefixes of the array, we can iterate through the array. The numbers before the iterated number and the iterated number together form the prefix.

To check whether the prefix satisfy the requirement, we need to examine the following three cases. All these three cases satisfy the requirement and all other cases will not satisfy the requirement.

1. All numbers in the prefix appear only once. For example: 1 2 3 4 5 6 7 8. In this case, we can remove any element and the remaining numbers all have the same occurrence frequency: 1.

2. Except for one number, all other number appear the same number of times. For example: 11 22 33 44 5. This is a more generic case of Case 1. We can remove the number that appears once, and the remaining array of numbers satisfy the requirement.

3. One number appears k+1 times, and the other numbers appear k times. For example: 111 222 3333. We can remove one of the 3s in the example, and the rest numbers satisfy the requirement.

These three cases are the only possible cases that satisfy the requirement. The reason is as follows. To construct a prefix to satisfy the requirement, we first need to have some numbers that appear the same number of times in the prefix. We then add one more number to the prefix, and can obtain an array satisfy the requirement. The one number added can be the same as one of the original numbers (Case 3), or can be a totally different number (Case 2, note that Case 1 is a special case of Case 2). This is the only way to construct such a prefix. Thus, we only need to check whether a prefix is any of the above 3 cases to see if it satisfy the requirement.


To check whether a prefix is any of the above 3 cases, we need to keep track of the occurrence frequency of each unique number. We also track the occurrence frequency of each unique frequency. For example, for the prefix 111 222 3333. The occurrence frequency of each unique number is: 1 -- 3 times, 2 -- 3 times, 3 -- 4 times. The occurrence frequency of each unique frequency is: freq 3 -- 2 times, freq 4 -- 1 time. This makes it easy for calculating how many numbers are there. We use two hash tables (freq for the first frequency and f_freq for the second frequency) to store these two frequencies. We also keep track of the maximum frequency (max_freq) we have so far.

To check Case 1, we just check whether max_freq = 1.
To check Case 2, we check: max_freq * f_freq[max_freq] + 1 = numbers in the prefix.
To check Case 3, we check: (max_freq - 1) * (f_freq[max_freq - 1] + 1) + 1 = numbers in the prefix.

If the prefix is any of the above 3 cases, we can record the length of the prefix.

The time complexity is O(n), and the space complexity is O(n).



<br />

## Sample C++ Code


This is a C++ implementation of the hash table approach.

```c
#include <iostream>
#include <vector>
#include <map>
#include <algorithm>

using namespace std;

int maxEqualFreq(vector<int>& nums) {
    int n = nums.size();
    // If nums is empty, we return 0.
    // If only one number exists, it satisfy the requirement. We return 1.
    if (n <= 1) return n;  
    
    int max_len = 0;
    
    map<int, int> freq;
    map<int, int> f_freq;
    
    int max_freq = 0;
    for (int i = 0; i < n; i ++) {
        if (freq.find(nums[i]) == freq.end())
            freq[nums[i]] = 0;
        freq[nums[i]] ++;
        
        // Update the occurrence frequencies of the frequencies
        f_freq[freq[nums[i]] - 1] --;
        f_freq[freq[nums[i]]] ++;
        
        max_freq = max(max_freq, freq[nums[i]]);

        // Whether the prefix is any of the 3 cases
        if ((max_freq == 1) || (max_freq*f_freq[max_freq]+1 == i+1) || ((max_freq-1)*(f_freq[max_freq-1]+1)+1 == i+1)) {
            max_len = i + 1;
        }
        
    }
    return max_len;
}

int main() {
    vector<int> nums = {10,2,8,9,3,8,1,5,2,3,7,6};
    cout << maxEqualFreq(nums) << endl;
}
```
