---
layout: post
title: "To Lower Case Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 709. Given a string s, return the string after replacing every uppercase letter with the same lowercase letter.

---

<br />

## Description

LeetCode Problem 709.

Given a string s, return the string after replacing every uppercase letter with the same lowercase letter.

Example 1:
```
Input: s = "Hello"
Output: "hello"
```

Example 2:
```
Input: s = "here"
Output: "here"
```

Example 3:
```
Input: s = "LOVELY"
Output: "lovely"
```

Constraints:
* 1 <= s.length <= 100
* s consists of printable ASCII characters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string toLowerCase(string str) {        
        for (char& c : str) {
            if (c >= 'A' && c <= 'Z') c += 32;
        }
        return str;
    }
};
```


