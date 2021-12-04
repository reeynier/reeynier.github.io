---
layout: post
title: "Evaluate Reverse Polish Notation Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Stack ]
similar: [ Stack ]
featured: false
hidden: false
excerpt: LeetCode 150. Evaluate the value of an arithmetic expression in Reverse Polish Notation.

---

<br />

## Description

LeetCode Problem 150.

Evaluate the value of an arithmetic expression in  Reverse Polish Notation.

Valid operators are +, -, *, and /. Each operand may be an integer or another expression.

Note that division between two integers should truncate toward zero.

It is guaranteed that the given RPN expression is always valid. That means the expression would always evaluate to a result, and there will not be any division by zero operation.

Example 1:
```
Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```

Example 2:
```
Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```

Example 3:
```
Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

Constraints:
* 1 <= tokens.length <= 10^4
* tokens[i] is either an operator: "+", "-", "*", or "/", or an integer in the range [-200, 200].

<br />

## Sample C++ Code


```c
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> st;
        int i = 0, num1, num2;
        while (i < tokens.size()) {
            if (tokens[i] == "+" || 
                tokens[i] == "-" || 
                tokens[i] == "*" || 
                tokens[i] == "/") {
                num2 = st.top();
                st.pop();
                num1 = st.top();
                st.pop();
                if (tokens[i] == "+")
                    st.push(num1 + num2);
                if (tokens[i] == "-")
                    st.push(num1 - num2);
                if (tokens[i] == "*")
                    st.push(num1 * num2);
                if (tokens[i] == "/")
                    st.push(num1 / num2);
            } else {
                st.push(stoi(tokens[i]));
            }
            i ++;
        }
        return st.top();
    }
};
```


