---
layout: post
title: "Find K Closest Elements Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Two Pointers, Binary Search, Sorting, Heap ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 658. Given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The result should also be sorted in ascending order.

---

<br />

## Description

LeetCode Problem 658.

Given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The result should also be sorted in ascending order.

An integer a is closer to x than an integer b if:
* |a - x| < |b - x|, or
* |a - x| == |b - x| and a < b

Example 1:
```
Input: arr = [1,2,3,4,5], k = 4, x = 3
Output: [1,2,3,4]
```

Example 2:
```
Input: arr = [1,2,3,4,5], k = 4, x = -1
Output: [1,2,3,4]
```

Constraints:
* 1 <= k <= arr.length
* 1 <= arr.length <= 10^4
* arr is sorted in ascending order.
* -10^4 <= arr[i], x <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> findClosestElements(vector<int>& arr,int k, int x) {
        int len = arr.size();
        if (len == 0)
            return {};
        
        int idx = upper_bound(arr.begin(), arr.end(), x) - arr.begin();
        vector<int> ans;
        int l = idx - 1, r = idx;
        while (k && (l >= 0) && (r <= len-1)) {
            k --;
            if (arr[r] - x >= x - arr[l]) {
                ans.push_back(arr[l--]);
            }
            else {
                ans.push_back(arr[r++]);
            }
        }
        while (k && (l >= 0)) {
            k --;
            ans.push_back(arr[l--]);
        }
        
        while (k && (r <= len - 1)) {
            k --;
            ans.push_back(arr[r++]);
        }
        sort(ans.begin(), ans.end());
        return ans;
    }
};
```


