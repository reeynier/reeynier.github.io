---
layout: post
title: "Longest Turbulent Subarray Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Sliding Window ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 978. Given an integer array arr, return the length of a maximum size turbulent subarray of arr.

---

<br />

## Description

LeetCode Problem 978.

Given an integer array arr, return the length of a maximum size turbulent subarray of arr.
A subarray is turbulent if the comparison sign flips between each adjacent pair of elements in the subarray.

More formally, a subarray [arr[i], arr[i + 1], ..., arr[j]] of arr is said to be turbulent if and only if:
* For i <= k < j:
* arr[k] > arr[k + 1] when k is odd, and
* arr[k] < arr[k + 1] when k is even.
* Or, for i <= k < j:
* arr[k] > arr[k + 1] when k is even, and
* arr[k] < arr[k + 1] when k is odd.

Example 1:
```
Input: arr = [9,4,2,10,7,8,8,1,9]
Output: 5
Explanation: arr[1] > arr[2] < arr[3] > arr[4] < arr[5]
```

Example 2:
```
Input: arr = [4,8,12,16]
Output: 2
```

Example 3:
```
Input: arr = [100]
Output: 1
```

Constraints:
* 1 <= arr.length <= 4 * 10^4
* 0 <= arr[i] <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maxTurbulenceSize(vector<int>& arr) {
        int n = arr.size();
        if (n < 2) return n;
        
        int total = 1, maxim = 0;
        
        for (int i = 1; i < n; i++) {
            if (arr[i] != arr[i-1]) total++;
            
            while (i < n-1 && (arr[i] - arr[i-1]) / 10000.0 * (arr[i] - arr[i+1]) / 10000.0 > 0) { 
                //division by 10000.0 to avoid integer overflow.
                total++;
                i++;
            }
            maxim = max(total,maxim);
            total = 1;
        }
        return maxim;
    }
};
```


