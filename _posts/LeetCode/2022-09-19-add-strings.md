---
layout: post
title: "Add Strings Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, String, Simulation ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 415. Given two non-negative integers, num1 and num2 represented as string, return the sum of num1 and num2 as a string.

---

<br />

## Description

LeetCode Problem 415.

Given two non-negative integers, num1 and num2 represented as string, return the sum of num1 and num2 as a string.

You must solve the problem without using any built-in library for handling large integers (such as BigInteger). You must also not convert the inputs to integers directly.

Example 1:
```
Input: num1 = "11", num2 = "123"
Output: "134"
```

Example 2:
```
Input: num1 = "456", num2 = "77"
Output: "533"
```

Example 3:
```
Input: num1 = "0", num2 = "0"
Output: "0"
```

Constraints:
* 1 <= num1.length, num2.length <= 10^4
* num1 and num2 consist of only digits.
* num1 and num2 don't have any leading zeros except for the zero itself.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string addStrings(string num1, string num2) {
        int len1 = num1.size();
        int len2 = num2.size();
        int len = max(len1, len2);
        int c = 0;
        int s = 0;
        string sum;
        
        for (int i = 0; i < len; i ++) {
            s = c;
            if (i < len1)
                s += num1[len1 - i - 1] - '0';
            if (i < len2)
                s += num2[len2 - i - 1] - '0';  
            c = s / 10;
            s = s % 10;
            sum += to_string(s);
        }
        
        if (c != 0)
            sum += to_string(c);
        
        reverse(sum.begin(), sum.end());
        
        return sum;
    }
};
```


