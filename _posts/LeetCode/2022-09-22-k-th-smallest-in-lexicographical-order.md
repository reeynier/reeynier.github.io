---
layout: post
title: "K-Th Smallest In Lexicographical Order Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 440. Given two integers n and k, return the k^th lexicographically smallest integer in the range [1, n].

---

<br />

## Description

LeetCode Problem 440.

Given two integers n and k, return the k^th lexicographically smallest integer in the range [1, n].

Example 1:
```
Input: n = 13, k = 2
Output: 10
Explanation: The lexicographical order is [1, 10, 11, 12, 13, 2, 3, 4, 5, 6, 7, 8, 9], so the second smallest number is 10.
```

Example 2:
```
Input: n = 1, k = 1
Output: 1
```

Constraints:
* 1 <= k <= n <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    long long get_count(long long prefix, long long n){
        long long upper = prefix + 1, cnt = 0;
        while (prefix <= n) {
            cnt += min(n + 1, upper) - prefix;
            prefix *= 10;
            upper *= 10;
        }
        return cnt;
    }

    int findKthNumber(int n, int k) {
        int prefix = 1, cnt = 1;
        while (cnt < k) {
            int tmpcnt = get_count(prefix, n);
            if (tmpcnt + cnt <= k) {
                prefix ++;
                cnt += tmpcnt;
            } else {
                prefix *= 10;
                cnt ++;
            }
        }
        return prefix;
    }
};
```


