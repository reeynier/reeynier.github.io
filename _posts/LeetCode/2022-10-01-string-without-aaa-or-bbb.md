---
layout: post
title: "String Without Aaa Or Bbb Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Greedy ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 984. Given two integers a and b, return any string s such that

---

<br />

## Description

LeetCode Problem 984.

Given two integers a and b, return any string s such that:
* s has length a + b and contains exactly a 'a' letters, and exactly b 'b' letters,
* The substring 'aaa' does not occur in s, and
* The substring 'bbb' does not occur in s.

Example 1:
```
Input: a = 1, b = 2
Output: "abb"
Explanation: "abb", "bab" and "bba" are all correct answers.
```

Example 2:
```
Input: a = 4, b = 1
Output: "aabaa"
```

Constraints:
* 0 <= a, b <= 100
* It is guaranteed such an s exists for the given a and b.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string strWithout3a3b(int A, int B) {
        string res;
        while (A && B) {
            if (A > B) {
                res += "aab";
                A--;
            } else if (B > A) {
                res += "bba";
                B--;
            } else {
                res += "ab";
            }
            A--;
            B--;
        }
        while (A--) 
            res += "a";
        while (B--) 
            res += "b";
        return res;
    }
};
```


