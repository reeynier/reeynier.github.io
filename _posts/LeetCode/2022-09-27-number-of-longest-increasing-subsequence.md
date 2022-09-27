---
layout: post
title: "Number Of Longest Increasing Subsequence Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Binary Indexed Tree, Segment Tree ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 673. Given an integer arraynums, return the number of longest increasing subsequences.

---

<br />

## Description

LeetCode Problem 673.

Given an integer arraynums, return the number of longest increasing subsequences.

Notice that the sequence has to be strictly increasing.

Example 1:
```
Input: nums = [1,3,5,4,7]
Output: 2
Explanation: The two longest increasing subsequences are [1, 3, 4, 7] and [1, 3, 5, 7].
```

Example 2:
```
Input: nums = [2,2,2,2,2]
Output: 5
Explanation: The length of longest continuous increasing subsequence is 1, and there are 5 subsequences' length is 1, so output 5.
```

Constraints:
* 1 <= nums.length <= 2000
* -10^6 <= nums[i] <= 10^6

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findNumberOfLIS(vector<int>& nums) {
        const int n = nums.size();
        // stores length of longest sequence till i-th position
        vector<int> lis(n,1);  
        // stores count of longest sequence of length lis[i]
        vector<int> count(n,1);  
        // maximum length of lis
        int maxLen = 1;  
		
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    if (lis[j] + 1 > lis[i]) { 
                        // strictly increasing
                        lis[i] = lis[j] + 1;
                        count[i] = count[j];
                    } 
                    // this means there are more subsequences of same length ending at length lis[i]
                    else if (lis[j] + 1 == lis[i]) { 
                        count[i] += count[j];
                    }
                }
            }
            maxLen = max(maxLen, lis[i]);
        }
        
        int numOfLIS = 0;
        // count all the subseq of length maxLen
        for (int i = 0; i < n; i++) {
            if (lis[i] == maxLen)
                numOfLIS += count[i];
        }
            
        return numOfLIS;
    }
};
```


