---
layout: post
title:  "Valid Parentheses Problem"
categories: [ Data Structure ]
tags: [ Stack, String, Leetcode ]
similar: [ Stack ]
featured: false
hidden: false
excerpt: LeetCode 20. Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
---

<br />

## Description

LeetCode Problem 20. 

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

* Open brackets must be closed by the same type of brackets.
* Open brackets must be closed in the correct order.
 

Example 1:
```
Input: s = "()"
Output: true
```

Example 2:
```
Input: s = "()[]{}"
Output: true
```

Example 3:
```
Input: s = "(]"
Output: false
```

Example 4:
```
Input: s = "([)]"
Output: false
```

Example 5:
```
Input: s = "{[]}"
Output: true
```

Constraints:

* 1 <= s.length <= 10^4
* s consists of parentheses only '()[]{}'.


<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isValid(string s) {
        stack<char> paren;
        for (char c: s) {
            if ((c == '(') || (c == '[') || (c == '{')) {
                paren.push(c);
            } else {
                if (paren.empty())
                    return false;
                if ((c == ')') && paren.top() != '(')
                    return false;
                if ((c == ']') && paren.top() != '[')
                    return false;
                if ((c == '}') && paren.top() != '{')
                    return false;
                paren.pop();
            }
        }
        if (paren.empty())
            return true;
        else 
            return false;
    }
    
};
```
