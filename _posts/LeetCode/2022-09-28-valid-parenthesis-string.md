---
layout: post
title: "Valid Parenthesis String Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Dynamic Programming, Stack, Greedy ]
similar: [ Stack ]
featured: false
hidden: false
excerpt: LeetCode 678. Given a string s containing only three types of characters '(', ')' and '\*', return true if s is valid.

---

<br />

## Description

LeetCode Problem 678.

Given a string s containing only three types of characters: '(', ')' and '\*', return true if s is valid.

The following rules define a valid string:
* Any left parenthesis '(' must have a corresponding right parenthesis ')'.
* Any right parenthesis ')' must have a corresponding left parenthesis '('.
* Left parenthesis '(' must go before the corresponding right parenthesis ')'.
* '\*' could be treated as a single right parenthesis ')' or a single left parenthesis '(' or an empty string "".

Example 1:
```
Input: s = "()"
Output: true
```

Example 2:
```
Input: s = "(*)"
Output: true
```

Example 3:
```
Input: s = "(*))"
Output: true
```

Constraints:
* 1 <= s.length <= 100
* s[i] is '(', ')' or '\*'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool checkValidString(string s) {
        int lower = 0, upper = 0;
        for (char c : s) {
            if (c == '(') {
                lower ++;
                upper ++;
            } else if (c == ')') {
                lower --;               
                upper --;
            } else { 
                // * encountered
                lower --;
                upper ++;
            }
            lower = max(lower, 0);
            if (upper < 0) 
                // unmatched ')' found in the middle of string
                return false;
        }
        return lower == 0;
    }
};
```


