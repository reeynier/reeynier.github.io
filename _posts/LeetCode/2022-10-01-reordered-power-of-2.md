---
layout: post
title: "Reordered Power Of 2 Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Sorting, Counting ]
similar: [ Sorting ]
featured: false
hidden: false
excerpt: LeetCode 869. You are given an integer n. We reorder the digits in any order (including the original order) such that the leading digit is not zero.

---

<br />

## Description

LeetCode Problem 869.

You are given an integer n. We reorder the digits in any order (including the original order) such that the leading digit is not zero.

Return true if and only if we can do this so that the resulting number is a power of two.

Example 1:
```
Input: n = 1
Output: true
```

Example 2:
```
Input: n = 10
Output: false
```

Example 3:
```
Input: n = 16
Output: true
```

Example 4:
```
Input: n = 24
Output: false
```

Example 5:
```
Input: n = 46
Output: true
```

Constraints:
* 1 <= n <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool reorderedPowerOf2(int N) {
        string N_str = sorted_num(N);
        for (int i = 0; i < 32; i++)
            if (N_str == sorted_num(1 << i)) 
                return true;
        return false;
    }
    
    string sorted_num(int n) {
        string res = to_string(n);
        sort(res.begin(), res.end());
        return res;
    }
};
```


