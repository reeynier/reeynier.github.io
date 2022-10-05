---
layout: post
title: "Shortest Subarray With Sum At Least K Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search, Queue, Sliding Window, Heap ]
similar: [ Heap ]
featured: false
hidden: false
excerpt: LeetCode 862. Given an integer array nums and an integer k, return the length of the shortest non-empty subarray of nums with a sum of at least k. If there is no such subarray, return -1.

---

<br />

## Description

LeetCode Problem 862.

Given an integer array nums and an integer k, return the length of the shortest non-empty subarray of nums with a sum of at least k. If there is no such subarray, return -1.

A subarray is a contiguous part of an array.

Example 1:
```
Input: nums = [1], k = 1
Output: 1
```

Example 2:
```
Input: nums = [1,2], k = 4
Output: -1
```

Example 3:
```
Input: nums = [2,-1,2], k = 3
Output: 3
```

Constraints:
* 1 <= nums.length <= 10^5
* -10^5 <= nums[i] <= 10^5
* 1 <= k <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    int shortestSubarray(vector<int>& A, int K) {
        priority_queue<pair<long long, long long>, vector<pair<long long, long long>>, greater<pair<long long, long long>> > pq;
        long long sum = 0;
        long long ans = 1e18;
        for (long long i = 0; i < A.size(); i++) {
            sum += (long long)A[i];
            if (sum >= K) {
                ans = min(ans, i + 1);
            }
            while (pq.size() && sum - pq.top().first >= K) {
                auto &p = pq.top();
                ans = min(ans, i - p.second);
                pq.pop();
            }
            pq.push({sum, i});
        }
        return ans == 1e18 ? -1 : ans;
    }
};
```


