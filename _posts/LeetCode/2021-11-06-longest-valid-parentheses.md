---
layout: post
title:  "Longest Valid Parentheses Problem"
categories: [ Data Structure ]
tags: [ String, Dynamic Programming, Stack Leetcode ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 32. Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.
---

<br />

## Description

LeetCode Problem 32. 

Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

 

Example 1:
```
Input: s = "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()".
```

Example 2:
```
Input: s = ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()".
```

Example 3:
```
Input: s = ""
Output: 0
```

Constraints:

* 0 <= s.length <= 3 * 10^4
* s[i] is '(', or ')'.


<br />

## Sample C++ Code


```c
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> stk;
        stk.push(-1);
        int ans = 0;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(') {
                stk.push(i);
            } else {
                stk.pop();
                if (stk.empty()) {
                    stk.push(i);
                } else {
                    ans = max(ans, i - stk.top());
                }
            }
        }
        return ans;
    }
};
```
