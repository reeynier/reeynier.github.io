---
layout: post
title: "Sum Of Subarray Minimums Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Stack ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 907. Given an array of integers arr, find the sum of min(b), where b ranges over every (contiguous) subarray of arr. Since the answer may be large, return the answer modulo 10^9 + 7.

---

<br />

## Description

LeetCode Problem 907.

Given an array of integers arr, find the sum of min(b), where b ranges over every (contiguous) subarray of arr. Since the answer may be large, return the answer modulo 10^9 + 7.

Example 1:
```
Input: arr = [3,1,2,4]
Output: 17
Explanation: 
Subarrays are [3], [1], [2], [4], [3,1], [1,2], [2,4], [3,1,2], [1,2,4], [3,1,2,4]. 
Minimums are 3, 1, 2, 4, 1, 1, 2, 1, 1, 1.
Sum is 17.
```

Example 2:
```
Input: arr = [11,81,94,43,3]
Output: 444
```

Constraints:
* 1 <= arr.length <= 3 * 10^4
* 1 <= arr[i] <= 3 * 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int sumSubarrayMins(vector<int>& arr) {
        int n = arr.size(), mod = 1e9 + 7;
        long sum = 0;
        stack<pair<int, long>> sums;
        for (int i = n - 1; i >= 0; i--) {
            while (!sums.empty() && arr[i] <= arr[sums.top().first]) 
                sums.pop();
            if (sums.empty()) 
                sums.push({i, (arr[i] * (n - i)) % mod});
            else 
                sums.push({i, (sums.top().second + arr[i] * (sums.top().first - i)) % mod});
            sum = (sum + sums.top().second) % mod;
        }
        return sum % mod;
    }
};
```


