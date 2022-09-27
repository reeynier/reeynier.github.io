---
layout: post
title: "Rotate String Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 796. Given two strings s and goal, return true if and only if s can become goal after some number of shifts on s.

---

<br />

## Description

LeetCode Problem 796.

Given two strings s and goal, return true if and only if s can become goal after some number of shifts on s.

A shift on s consists of moving the leftmost character of s to the rightmost position.
* For example, if s = "abcde", then it will be "bcdea" after one shift.

Example 1:
```
Input: s = "abcde", goal = "cdeab"
Output: true
```

Example 2:
```
Input: s = "abcde", goal = "abced"
Output: false
```

Constraints:
* 1 <= s.length, goal.length <= 100
* s and goal consist of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool rotateString(string A, string B) {
        if (A.size() != B.size())
            return false;
        if (A == B)      
            //for empty strings
            return true;
        
        int len = B.size();
        while (len--) {
            if (A == B)
                return true;
            // one shift on A
            A = A.substr(1) + A[0];     
        }
        return false;
    }
};
```


