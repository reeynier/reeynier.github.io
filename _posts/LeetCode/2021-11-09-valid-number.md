---
layout: post
title:  "Valid Number Problem"
categories: [ Data Structure ]
tags: [ String, Leetcode ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 65. Given a string s, return true if s is a valid number.
---

<br />

## Description

LeetCode Problem 65. 

A valid number can be split up into these components (in order):

* A decimal number or an integer.
* (Optional) An 'e' or 'E', followed by an integer.

A decimal number can be split up into these components (in order):

* (Optional) A sign character (either '+' or '-').
* One of the following formats:
    + One or more digits, followed by a dot '.'.
    + One or more digits, followed by a dot '.', followed by one or more digits.
    + A dot '.', followed by one or more digits.

An integer can be split up into these components (in order):

* (Optional) A sign character (either '+' or '-').
* One or more digits.

For example, all the following are valid numbers: ["2", "0089", "-0.1", "+3.14", "4.", "-.9", "2e10", "-90E3", "3e+7", "+6e-1", "53.5e93", "-123.456e789"], while the following are not valid numbers: ["abc", "1a", "1e", "e3", "99e2.5", "--6", "-+3", "95a54e53"].

Given a string s, return true if s is a valid number.

 

Example 1:
```
Input: s = "0"
Output: true
```

Example 2:
```
Input: s = "e"
Output: false
```

Example 3:
```
Input: s = "."
Output: false
```

Example 4:
```
Input: s = ".1"
Output: true
```
 

Constraints:

* 1 <= s.length <= 20
* s consists of only English letters (both uppercase and lowercase), digits (0-9), plus '+', minus '-', or dot '.'.



<br />

## Sample C++ Code


```c
bool isNumber(const char *s) 
{
    /* 
    1. skip the leading whitespaces;
    2. check if the significand is valid. To do so, simply skip the leading sign and 
        count the number of digits and the number of points. A valid significand has 
        no more than one point and at least one digit.
    3. check if the exponent part is valid. We do this if the significand is followed 
        by 'e'. Simply skip the leading sign and count the number of digits. 
        A valid exponent contain at least one digit.
    4. skip the trailing whitespaces. We must reach the ending 0 if the string is a valid number. 
    */
    int i = 0;
    
    // skip the whilespaces
    for(; s[i] == ' '; i++) {}
    
    // check the significand
    if(s[i] == '+' || s[i] == '-') 
        // skip the sign if exist
        i++; 
    
    int n_nm, n_pt;
    for(n_nm=0, n_pt=0; (s[i]<='9' && s[i]>='0') || s[i]=='.'; i++)
        s[i] == '.' ? n_pt++:n_nm++;       
    if(n_pt>1 || n_nm<1) 
    // no more than one point, at least one digit
        return false;
    
    // check the exponent if exist
    if(s[i] == 'e') {
        i++;
        if(s[i] == '+' || s[i] == '-') i++; // skip the sign
        
        int n_nm = 0;
        for(; s[i]>='0' && s[i]<='9'; i++, n_nm++) {}
        if(n_nm<1)
            return false;
    }
    
    // skip the trailing whitespaces
    for(; s[i] == ' '; i++) {}
    
    // must reach the ending 0 of the string
    return s[i]==0;  
}
```
