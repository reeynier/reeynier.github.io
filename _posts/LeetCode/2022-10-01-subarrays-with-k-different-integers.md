---
layout: post
title: "Subarrays With K Different Integers Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Sliding Window, Counting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 992. Given an integer array nums and an integer k, return the number of good subarrays of nums.

---

<br />

## Description

LeetCode Problem 992.

Given an integer array nums and an integer k, return the number of good subarrays of nums.

A good array is an array where the number of different integers in that array is exactly k.
* For example, [1,2,3,1,2] has 3 different integers: 1, 2, and 3.

A subarray is a contiguous part of an array.

Example 1:
```
Input: nums = [1,2,1,2,3], k = 2
Output: 7
Explanation: Subarrays formed with exactly 2 different integers: [1,2], [2,1], [1,2], [2,3], [1,2,1], [2,1,2], [1,2,1,2]
```

Example 2:
```
Input: nums = [1,2,1,3,4], k = 3
Output: 3
Explanation: Subarrays formed with exactly 3 different integers: [1,2,1,3], [2,1,3], [1,3,4].
```

Constraints:
* 1 <= nums.length <= 2 * 10^4
* 1 <= nums[i], k <= nums.length

<br />

## Sample C++ Code


```c
class Solution {
public:
    int upToK(vector<int>& A, int K) {
        int len = A.size();
        unordered_map<int, int> m;
        for (int i = 0; i < len; i ++) {
            m[A[i]] = 0;
        }
        
        int cntdiff = 0;
        int ans = 0;
        int i = 0, j = 0;
        while (j < len) {
            m[A[j]] ++;
            if (m[A[j]] == 1) cntdiff ++;
            
            while (cntdiff > K) {
                m[A[i]] --;
                if (m[A[i]] == 0) cntdiff --;
                i ++;
            }
    
            ans += j - i;
            j ++;
        }
        return ans;
    }
    
    int subarraysWithKDistinct(vector<int>& A, int K) {
        return upToK(A, K) - upToK(A, K-1);
    }
};
```


