---
layout: post
title: "Solve The Equation Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, String, Simulation ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 640. Solve a given equation and return the value of 'x' in the form of a string "x=#value". The equation contains only '+', '-' operation, the variable 'x' and its coefficient. You should return "No solution" if there is no solution for the equation, or "Infinite solutions" if there are infinite solutions for the equation.

---

<br />

## Description

LeetCode Problem 640.

Solve a given equation and return the value of 'x' in the form of a string "x=#value". The equation contains only '+', '-' operation, the variable 'x' and its coefficient. You should return "No solution" if there is no solution for the equation, or "Infinite solutions" if there are infinite solutions for the equation.

If there is exactly one solution for the equation, we ensure that the value of 'x' is an integer.

Example 1:
```
Input: equation = "x+5-3+x=6+x-2"
Output: "x=2"
```

Example 2:
```
Input: equation = "x=x"
Output: "Infinite solutions"
```

Example 3:
```
Input: equation = "2x=x"
Output: "x=0"
```

Example 4:
```
Input: equation = "2x+3x-6x=x+2"
Output: "x=-1"
```

Example 5:
```
Input: equation = "x=x+2"
Output: "No solution"
```

Constraints:
* 3 <= equation.length <= 1000
* equation has exactly one '='.
* equation consists of integers with an absolute value in the range [0, 100] without any leading zeros, and the variable 'x'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string solveEquation(string equation) {
        int i = 0;
        int para = 0, xpara = 0;
        int flag = 1;
        while (i < equation.size()) {
            int sign = 1;
            int temp = 0;
            if (equation[i] == '=') {
                flag = -1;
                i ++;
            }
            if (equation[i] == '-') {
                sign = -1; 
                i ++;
            }
            if (equation[i] == '+') {
                sign = 1;
                i ++;
            }
            
            if (isdigit(equation[i])) {
                while (i < equation.size() && isdigit(equation[i])) {
                    temp = temp * 10 + equation[i] - '0';
                    i ++;
                }
                if (i < equation.size() && equation[i] == 'x') {
                    xpara += flag * sign * temp;
                    i ++;
                } 
                else 
                    para += flag * sign * temp;
            } 
            else {
                xpara += flag * sign;
                i ++;
            }
            
        }
        
        string res;
        if (para == 0 && xpara == 0) 
            res = "Infinite solutions";
        else if (xpara == 0) 
            res = "No solution";
        else
            res = "x=" + to_string(para / xpara * -1);
        
        return res;
    }
};
```


