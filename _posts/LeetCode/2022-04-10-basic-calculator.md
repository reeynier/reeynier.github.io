---
layout: post
title: "Basic Calculator Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, String, Stack, Recursion ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 224. Given a string s representing a valid expression, implement a basic calculator to evaluate it, and return the result of the evaluation.

---

<br />

## Description

LeetCode Problem 224.

Given a string s representing a valid expression, implement a basic calculator to evaluate it, and return the result of the evaluation.

Note: You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as eval().

Example 1:
```
Input: s = "1 + 1"
Output: 2
```

Example 2:
```
Input: s = " 2-1 + 2 "
Output: 3
```

Example 3:
```
Input: s = "(1+(4+5+2)-3)+(6+8)"
Output: 23
```

Constraints:
* 1 <= s.length <= 3 * 10^5
* s consists of digits, '+', '-', '(', ')', and ' '.
* s represents a valid expression.
* '+' is not used as a unary operation (i.e., "+1" and "+(2 + 3)" is invalid).
* '-' could be used as a unary operation (i.e., "-1" and "-(2 + 3)" is valid).
* There will be no two consecutive operators in the input.
* Every number and running calculation will fit in a signed 32-bit integer.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int calculate(string s) {
        // the given expression is always valid, only + and - 
        // every + and - can be flipped base on it's depth in ().
        stack<int> signs;
        int sign = 1;
        int num = 0;
        int ans = 0;
        
        // always transform s into ( s )
        signs.push(1);
        
        for (auto c : s) {
            if (c >= '0' && c <= '9') {
                num = 10 * num + c - '0';
            } else if (c == '+' || c == '-') {
                ans = ans + signs.top() * sign * num;
                num = 0;
                sign = (c == '+' ? 1 : -1);
            } else if (c == '(') {
                signs.push(sign * signs.top());
                sign = 1;
            } else if (c == ')') {
                ans = ans + signs.top() * sign * num;
                num = 0;
                signs.pop();
                sign = 1;
            }
        }
        
        if (num) {
            ans = ans + signs.top() * sign * num;
        }
        
        return ans;
    }
};
```


