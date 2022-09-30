---
layout: post
title: "Binary Subarrays With Sum Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Sliding Window, Prefix Sum ]
similar: [ Sliding Window ]
featured: false
hidden: false
excerpt: LeetCode 930. Given a binary array nums and an integer goal, return the number of non-empty subarrays with a sum goal.

---

<br />

## Description

LeetCode Problem 930.

Given a binary array nums and an integer goal, return the number of non-empty subarrays with a sum goal.

A subarray is a contiguous part of the array.

Example 1:
```
Input: nums = [1,0,1,0,1], goal = 2
Output: 4
Explanation: The 4 subarrays are bolded and underlined below:
[1,0,1,0,1]
[1,0,1,0,1]
[1,0,1,0,1]
[1,0,1,0,1]
```

Example 2:
```
Input: nums = [0,0,0,0,0], goal = 0
Output: 15
```

Constraints:
* 1 <= nums.length <= 3 * 10^4
* nums[i] is either 0 or 1.
* 0 <= goal <= nums.length

<br />

## Sample C++ Code


```c
class Solution {
public:
    int numSubarraysWithSum(vector<int>& A, int S) {
        int left, right, sum, count;
        int last_left, next_left, right_start;
        
        count = 0;
        sum = 0;
        left = 0;
        right_start = 0;
        
        if (S == 0) {
            while ((A[right_start] == 1) && (right_start < A.size()))
                right_start ++;
        }
        
        last_left = right_start;
        next_left = right_start;
        
        for (right = right_start; right < A.size(); right++) {
            sum += A[right];
            if (sum == S) {
                break;
            }
        }
        if (sum < S)
            return 0;
        
        for (; right < A.size(); right++) {
            if (A[right] == 1) {
                last_left = next_left;
            }
            for (left = last_left; left < A.size(); left ++) {
                if (A[left] == 1) {
                    next_left = left + 1;
                    break;
                }
            }
            for (left = last_left; left <= right; left ++) {
                count ++;
                if (A[left] == 1) {
                    break;
                }
            }
            
        }
        
        return count;
    }
};
```


