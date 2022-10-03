---
layout: post
title: "Score Of Parentheses Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Stack ]
similar: [ Stack ]
featured: false
hidden: false
excerpt: LeetCode 856. Given a balanced parentheses string s, return the score of the string.

---

<br />

## Description

LeetCode Problem 856.

Given a balanced parentheses string s, return the score of the string.

The score of a balanced parentheses string is based on the following rule:
* "()" has score 1.
* AB has score A + B, where A and B are balanced parentheses strings.
* (A) has score 2 * A, where A is a balanced parentheses string.

Example 1:
```
Input: s = "()"
Output: 1
```

Example 2:
```
Input: s = "(())"
Output: 2
```

Example 3:
```
Input: s = "()()"
Output: 2
```

Example 4:
```
Input: s = "(()(()))"
Output: 6
```

Constraints:
* 2 <= s.length <= 50
* s consists of only '(' and ')'.
* s is a balanced parentheses string.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int scoreOfParentheses(string S) {
        if (S == "()")
            return 1;
        int score = 0, len = S.size();
        int balance = 0;
        for (int i = 0; i < len; i ++) {
            if (S[i] == '(')
                balance ++;
            else 
                balance --;
            if ((balance == 0) && (i != len-1)){
                return scoreOfParentheses(S.substr(0, i+1)) + 
                    scoreOfParentheses(S.substr(i+1));
            }
        }
        return 2 * scoreOfParentheses(S.substr(1, len-2));
    }
};
```


