---
layout: post
title: "Minimum Add To Make Parentheses Valid Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Stack, Greedy ]
similar: [ Stack ]
featured: false
hidden: false
excerpt: LeetCode 921. A parentheses string is valid if and only if

---

<br />

## Description

LeetCode Problem 921.

A parentheses string is valid if and only if:
* It is the empty string,
* It can be written as AB (A concatenated with B), where A and B are valid strings, or
* It can be written as (A), where A is a valid string.

You are given a parentheses string s. In one move, you can insert a parenthesis at any position of the string.

* For example, if s = "()))", you can insert an opening parenthesis to be "(()))" or a closing parenthesis to be "())))".

Return the minimum number of moves required to make s valid.

Example 1:
```
Input: s = "())"
Output: 1
```

Example 2:
```
Input: s = "((("
Output: 3
```

Example 3:
```
Input: s = "()"
Output: 0
```

Example 4:
```
Input: s = "()))(("
Output: 4
```

Constraints:
* 1 <= s.length <= 1000
* s[i] is either '(' or ')'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int minAddToMakeValid(string S) {
        int res = 0, n = S.size(), balance = 0;
        for (int i = 0; i < n; i++) {
            balance += S[i] == '(' ? 1 : -1;
            if (balance == -1) {
                res++;
                balance++;
            }
        }
        return res + balance;
    }
};
```


