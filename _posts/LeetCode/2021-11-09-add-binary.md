---
layout: post
title:  "Valid Number Problem"
categories: [ Data Structure ]
tags: [ String, Leetcode ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 67. A robot is located at the top-left corner of a m x n grid.
---

<br />

## Description

LeetCode Problem 67. 

Given two binary strings a and b, return their sum as a binary string.


Example 1:
```
Input: a = "11", b = "1"
Output: "100"
```

Example 2:
```
Input: a = "1010", b = "1011"
Output: "10101"
```
 

Constraints:

* 1 <= a.length, b.length <= 10^4
* a and b consist only of '0' or '1' characters.
* Each string does not contain leading zeros except for the zero itself.


<br />

## Sample C++ Code


```c
class Solution {
public:
    string addBinary(string a, string b) {
        int len1 = a.size(), len2 = b.size();
        int maxLen = max(len1, len2);
        string result;
        int s = 0, c = 0;
        
        for (int i = 0; i < maxLen; i ++) {
            s = c;
            if (i < len1)
                s += a[len1 - i - 1] - '0';
            if (i < len2)
                s += b[len2 - i - 1] - '0';
            c = s / 2;
            s = s % 2;
            result += to_string(s);
        }
        
        if (c != 0)
            result += to_string(c);
        
        reverse(result.begin(), result.end());
        return result;
    }
};
```
