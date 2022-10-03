---
layout: post
title: "Prime Palindrome Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 866. Given an integer n, return the smallest prime palindrome greater than or equal to n.

---

<br />

## Description

LeetCode Problem 866.

Given an integer n, return the smallest prime palindrome greater than or equal to n.

An integer is prime if it has exactly two divisors: 1 and itself. Note that 1 is not a prime number.
* For example, 2, 3, 5, 7, 11, and 13 are all primes.
An integer is a palindrome if it reads the same from left to right as it does from right to left.
* For example, 101 and 12321 are palindromes.

The test cases are generated so that the answer always exists and is in the range [2, 2 * 10^8].

Example 1:
```
Input: n = 6
Output: 7
```

Example 2:
```
Input: n = 8
Output: 11
```

Example 3:
```
Input: n = 13
Output: 101
```

Constraints:
* 1 <= n <= 10^8

<br />

## Sample C++ Code


```c
class Solution {
public:
    int evenPalindrome(int num) {
        string str1 = to_string(num);
        string str2 = str1;
        reverse(str2.begin(), str2.end());
        return stoi(str1 + str2);
    }

    int oddPlaindrome(int num) {
        string str1 = to_string(num);
        string str2 = str1.substr(0, str1.length() - 1);
        reverse(str2.begin(), str2.end());
        return stoi(str1 + str2);
    }

    bool isPrime(int num) {
        if (num == 1) {
            return false;
        }
        for (int i = 2; i * i <= num; ++i) {
            if (num % i == 0) {
                return false;
            }
        }
        return true;
    }
    
public:
    int primePalindrome(int N) {
        int even = 1;
        int odd = 1;

        int cur = 0;
        do {
            int evenp = evenPalindrome(even);
            int oddp = oddPlaindrome(odd);
            cur = min(evenp, oddp);
            if (evenp < oddp) {
                ++even;
            } else {
                ++odd;
            }
        } while (!(cur >= N && isPrime(cur)));

        return cur;
    }
};
```


