---
layout: post
title: "Find The Closest Palindrome Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 564. Given a string n representing an integer, return the closest integer (not including itself), which is a palindrome. If there is a tie, return the smaller one.

---

<br />

## Description

LeetCode Problem 564.

Given a string n representing an integer, return the closest integer (not including itself), which is a palindrome. If there is a tie, return the smaller one.

The closest is defined as the absolute difference minimized between two integers.

Example 1:
```
Input: n = "123"
Output: "121"
```

Example 2:
```
Input: n = "1"
Output: "0"
Explanation: 0 and 2 are the closest palindromes but we return the smallest which is 0.
```

Constraints:
* 1 <= n.length <= 18
* n consists of only digits.
* n does not have leading zeros.
* n is representing an integer in the range [1, 10^18 - 1].

<br />

## Sample C++ Code


```c
class Solution {
public:
    string makePalindromic(string s) {
        for (int i = 0, j = (int)s.length() - 1; i < j; i++, j--)
            s[j] = s[i];
        return s;
    }
    
    string nearestPalindromic(string n) {
        if (n == "0")
            return "1";
        
        long long orgVal = stoll(n);
    
        // candidate #1 (ex: 123xx -> 12321, 123xxx -> 123321)
        string res = makePalindromic(n);
        long long resVal = stoll(res);
        long long diff = abs(resVal - orgVal);
    
        long long scale = (long long)pow(10, (int)n.length() / 2);
    
        // candidate #2 (ex: 123xx -> 12221, 123xxx -> 122221, 100xx -> 9999)
        string smaller = makePalindromic(to_string((orgVal / scale) * scale - 1));
        // candidate #3 (ex: 123xx -> 12421, 123xxx -> 124421, 99xx -> 10001)
        string bigger = makePalindromic(to_string((orgVal / scale) * scale + scale));

        long long smallerVal = stoll(smaller);
        if (diff == 0 || abs(orgVal - smallerVal) <= diff) {
            res = smaller;
            diff = abs(orgVal - smallerVal);
        }

        long long biggerVal = stoll(bigger);
        if (abs(orgVal - biggerVal) < diff)
            res = bigger;
    
        return res;
    }
};
```


