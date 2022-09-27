---
layout: post
title: "Monotone Increasing Digits Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Greedy ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 738. An integer has monotone increasing digits if and only if each pair of adjacent digits x and y satisfy x <= y.

---

<br />

## Description

LeetCode Problem 738.

An integer has monotone increasing digits if and only if each pair of adjacent digits x and y satisfy x <= y.

Given an integer n, return the largest number that is less than or equal to n with monotone increasing digits.

Example 1:
```
Input: n = 10
Output: 9
```

Example 2:
```
Input: n = 1234
Output: 1234
```

Example 3:
```
Input: n = 332
Output: 299
```

Constraints:
* 0 <= n <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    int monotoneIncreasingDigits(int N) {
        string n_str = to_string(N);
        
        int marker = n_str.size();
        for (int i = n_str.size()-1; i > 0; i --) {
            if (n_str[i] < n_str[i-1]) {
                marker = i;
                n_str[i-1] = n_str[i-1]-1;
            }
        }
        
        for (int i = marker; i < n_str.size(); i ++) 
            n_str[i] = '9';
        
        return stoi(n_str);
    }
};
```


