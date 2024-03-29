---
layout: post
title: "3Sum With Multiplicity Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Two Pointers, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 923. Given an integer array arr, and an integer target, return the number of tuples i, j, k such that i < j < k and arr[i] + arr[j] + arr[k] == target.

---

<br />

## Description

LeetCode Problem 923.

Given an integer array arr, and an integer target, return the number of tuples i, j, k such that i < j < k and arr[i] + arr[j] + arr[k] == target.

As the answer can be very large, return it modulo 10^9 + 7.

Example 1:
```
Input: arr = [1,1,2,2,3,3,4,4,5,5], target = 8
Output: 20
Explanation: 
Enumerating by the values (arr[i], arr[j], arr[k]):
(1, 2, 5) occurs 8 times;
(1, 3, 4) occurs 8 times;
(2, 2, 4) occurs 2 times;
(2, 3, 3) occurs 2 times.
```

Example 2:
```
Input: arr = [1,1,2,2,2,2], target = 5
Output: 12
Explanation: 
arr[i] = 1, arr[j] = arr[k] = 2 occurs 12 times:
We choose one 1 from [1,1] in 2 ways,
and two 2s from [2,2,2,2] in 6 ways.
```

Constraints:
* 3 <= arr.length <= 3000
* 0 <= arr[i] <= 100
* 0 <= target <= 300

<br />

## Sample C++ Code


```c
class Solution {
public:
    int threeSumMulti(vector<int>& arr, int target) {
        unordered_map<int, int> m;
        int res = 0, mod = 1e9 + 7;
        for (int i = 0; i < arr.size(); i++) {
            res = (res + m[target - arr[i]]) % mod;
            for (int j = 0; j < i; j++) {
                m[arr[i] + arr[j]]++;
            }
        }
        return res;
    }
};
```


