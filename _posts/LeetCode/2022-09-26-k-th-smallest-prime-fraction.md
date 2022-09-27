---
layout: post
title: "K-Th Smallest Prime Fraction Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search, Sorting, Heap ]
similar: [ Heap ]
featured: false
hidden: false
excerpt: LeetCode 786. You are given a sorted integer array arr containing 1 and prime numbers, where all the integers of arr are unique. You are also given an integer k.

---

<br />

## Description

LeetCode Problem 786.

You are given a sorted integer array arr containing 1 and prime numbers, where all the integers of arr are unique. You are also given an integer k.

For every i and j where 0 <= i < j < arr.length, we consider the fraction arr[i] / arr[j].
Return the k^th smallest fraction considered. Return your answer as an array of integers of size 2, where answer[0] == arr[i] and answer[1] == arr[j].

Example 1:
```
Input: arr = [1,2,3,5], k = 3
Output: [2,5]
Explanation: The fractions to be considered in sorted order are:
1/5, 1/3, 2/5, 1/2, 3/5, and 2/3.
The third fraction is 2/5.
```

Example 2:
```
Input: arr = [1,7], k = 1
Output: [1,7]
```

Constraints:
* 2 <= arr.length <= 1000
* 1 <= arr[i] <= 3 * 10^4
* arr[0] == 1
* arr[i] is a prime number for i > 0.
* All the numbers of arr are unique and sorted in strictly increasing order.
* 1 <= k <= arr.length * (arr.length - 1) / 2

<br />

## Sample C++ Code using Priority Queue


```c
class Solution {
public:
    vector<int> kthSmallestPrimeFraction(vector<int>& A, int K) {
        priority_queue<pair<double, pair<int,int>>> pq;
        for (int i = 0; i < A.size(); i++)
            pq.push({-1.0*A[i]/A.back(), {i,A.size()-1}});
        while (--K > 0) {
            pair<int,int> cur = pq.top().second;
            pq.pop();
            cur.second--;
            pq.push({-1.0*A[cur.first]/A[cur.second], {cur.first, cur.second}});
        }
        return {A[pq.top().second.first], A[pq.top().second.second]};
    }
};
```


