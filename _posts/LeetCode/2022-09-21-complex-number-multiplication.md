---
layout: post
title: "Complex Number Multiplication Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, String, Simulation ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 537. A complex number can be represented as a string on the form "real+imaginaryi" where

---

<br />

## Description

LeetCode Problem 537.

A complex number can be represented as a string on the form "real+imaginaryi" where:
* real is the real part and is an integer in the range [-100, 100].
* imaginary is the imaginary part and is an integer in the range [-100, 100].
* i^2 == -1.

Given two complex numbers num1 and num2 as strings, return a string of the complex number that represents their multiplications.

Example 1:
```
Input: num1 = "1+1i", num2 = "1+1i"
Output: "0+2i"
Explanation: (1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i, and you need convert it to the form of 0+2i.
```

Example 2:
```
Input: num1 = "1+-1i", num2 = "1+-1i"
Output: "0+-2i"
Explanation: (1 - i) * (1 - i) = 1 + i2 - 2 * i = -2i, and you need convert it to the form of 0+-2i.
```

Constraints:
* num1 and num2 are valid complex numbers.

<br />

## Sample C++ Code


```c
class Solution {
public:
    pair<int, int> parse(string num) {
        int i = num.find('+');
        double real = stoi(num.substr(0, i));
        double imaginary = stoi(num.substr(i+1, num.size()-i-2));
        pair<int, int> res(real, imaginary);
        return res;
    }
    
    string complexNumberMultiply(string num1, string num2) {
        pair<int, int> a = parse(num1), b = parse(num2);
        int real_a = a.first, imag_a = a.second;
        int real_b = b.first, imag_b = b.second;
        
        return to_string(real_a * real_b - imag_a * imag_b) + '+' + to_string(real_a * imag_b  + real_b * imag_a)+'i' ;
    }
};
```


