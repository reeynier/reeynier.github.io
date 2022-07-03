---
layout: post
title: "Basic Calculator II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, String, Stack ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 227. Given a string s which represents an expression, evaluate this expression and return its value.

---

<br />

## Description

LeetCode Problem 227.

Given a string s which represents an expression, evaluate this expression and return its value.

The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of [-2^31, 2^31 - 1].

Note: You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as eval().

Example 1:
```
Input: s = "3+2*2"
Output: 7
```

Example 2:
```
Input: s = " 3/2 "
Output: 1
```

Example 3:
```
Input: s = " 3+5 / 2 "
Output: 5
```

Constraints:
* 1 <= s.length <= 3 * 10^5
* s consists of integers and operators ('+', '-', '*', '/') separated by some number of spaces.
* s represents a valid expression.
* All the integers in the expression are non-negative integers in the range [0, 2^31 - 1].
* The answer is guaranteed to fit in a 32-bit integer.

<br />

## Sample C++ Code


```c
 int calculate(string s) {
    stack<int> stk;
    int a;
    istringstream iss(s);
    char op = '+';
    while (iss >> a){
        if (op == '+' || op == '-'){
            stk.push(op == '+' ? a : -a);
        } 
        else{
            int last = stk.top();
            stk.pop();
            if (op == '*') last *= a;
            else last /= a;
            stk.push(last);
        }
        iss >> op;
    }
    int sum = 0;
    while(!stk.empty()){
        sum += stk.top();
        stk.pop();
    }
    return sum;
}
```


