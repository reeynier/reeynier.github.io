---
layout: post
title: "Ugly Number II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Math, Dynamic Programming, Heap ]
similar: [ Heap ]
featured: false
hidden: false
excerpt: LeetCode 264. An ugly number is a positive integer whose prime factors are limited to 2, 3, and 5.

---

<br />

## Description

LeetCode Problem 264.

An ugly number is a positive integer whose prime factors are limited to 2, 3, and 5.

Given an integer n, return the n^th ugly number.

Example 1:
```
Input: n = 10
Output: 12
Explanation: [1, 2, 3, 4, 5, 6, 8, 9, 10, 12] is the sequence of the first 10 ugly numbers.
```

Example 2:
```
Input: n = 1
Output: 1
Explanation: 1 has no prime factors, therefore all of its prime factors are limited to 2, 3, and 5.
```

Constraints:
* 1 <= n <= 1690

<br />

## Sample C++ Code


```c
class Solution {
public:
    int nthUglyNumber(int n) {
        priority_queue<long long int, vector<long long int>, greater<long long int>> pq;
        pq.push(1);
        
        int idx = 0;
        long long int top;
        while (idx < n) {
            top = pq.top();
            
            pq.push(top*2);
            pq.push(top*3);
            pq.push(top*5);
            
            while (!pq.empty() && pq.top() == top)
                pq.pop();
            
            idx ++;
        }
        return top;
    }
};
```


