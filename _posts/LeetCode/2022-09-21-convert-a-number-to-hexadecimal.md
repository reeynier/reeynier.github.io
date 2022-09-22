---
layout: post
title: "Convert A Number To Hexadecimal Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Bit Manipulation ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 405. Given an integer num, return a string representing its hexadecimal representation. For negative integers, two's complement method is used.

---

<br />

## Description

LeetCode Problem 405.

Given an integer num, return a string representing its hexadecimal representation. For negative integers, two's complement method is used.

All the letters in the answer string should be lowercase characters, and there should not be any leading zeros in the answer except for the zero itself.

Note:You are not allowed to use any built-in library method to directly solve this problem.

Example 1:
```
Input: num = 26
Output: "1a"
```

Example 2:
```
Input: num = -1
Output: "ffffffff"
```

Constraints:
* -2^31 <= num <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    const string HEX = "0123456789abcdef";
    string toHex(int num) {
        if (num == 0) return "0";
        string result;
        int count = 0;
        while (num && count++ < 8) {
            result = HEX[(num & 0xf)] + result;
            num >>= 4;
        }
        return result;
    }
};
```


