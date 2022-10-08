---
layout: post
title: "Super Palindromes Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 906. Let's say a positive integer is a super-palindrome if it is a palindrome, and it is also the square of a palindrome.

---

<br />

## Description

LeetCode Problem 906.

Let's say a positive integer is a super-palindrome if it is a palindrome, and it is also the square of a palindrome.

Given two positive integers left and right represented as strings, return the number of super-palindromes integers in the inclusive range [left, right].

Example 1:
```
Input: left = "4", right = "1000"
Output: 4
Explanation: 4, 9, 121, and 484 are superpalindromes.
Note that 676 is not a superpalindrome: 26 * 26 = 676, but 26 is not a palindrome.
```

Example 2:
```
Input: left = "1", right = "2"
Output: 1
```

Constraints:
* 1 <= left.length, right.length <= 18
* left and right consist of only digits.
* left and right cannot have leading zeros.
* left and right represent integers in the range [1, 10^18 - 1].
* left is less than or equal to right.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool check(long long n) {
        long long num = n, rev = 0, digit;
        do {
            digit = num % 10;
            rev = (rev * 10) + digit;
            num = num / 10;
        } while (num != 0);
        
        return rev == n;
    }
    
    long long nextPalindrome(long long palindrome, long long num) { 
        // if num = 123 this function will return 123321
        while (num > 0) {
            palindrome = palindrome * 10 + (num % 10);
            num /= 10;
        }
        return palindrome;
    }

    vector<long long> generatePalindromes(long long left, long long right) {
        vector<long long> res; 
        long long number;
        for (int i = 1; (number = nextPalindrome(i, i / 10)) <= right; i++) {
            if (number >= left && number <= right) 
                // odd palindrome 
                res.push_back(number); 
            number = nextPalindrome(i, i); 
            if (number >= left && number <= right) 
                // even palindrome
                res.push_back(number);
        }
        return res;
    }
    
    int superpalindromesInRange(string left, string right) {
        long long r = stoull(right), l = stoull(left);
        int cnt = 0;
        for (auto &ul : generatePalindromes(sqrt(l), sqrt(r)))
            if (check(ul * ul))
                cnt++;
        return cnt;
    }
};
```


