---
layout: post
title: "Valid Palindrome II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Two Pointers, String, Greedy ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 680. Given a string s, return true if the s can be palindrome after deleting at most one character from it.

---

<br />

## Description

LeetCode Problem 680.

Given a string s, return true if the s can be palindrome after deleting at most one character from it.

Example 1:
```
Input: s = "aba"
Output: true
```

Example 2:
```
Input: s = "abca"
Output: true
Explanation: You could delete the character 'c'.
```

Example 3:
```
Input: s = "abc"
Output: false
```

Constraints:
* 1 <= s.length <= 10^5
* s consists of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool validPalindrome(string s) {
        int lo = 0, hi = s.size() - 1;
        return validPalindrome(s, lo, hi, 0);
    }
    
    bool validPalindrome(string& s, int lo, int hi, int count) {
        if (count > 1) return false;
        while (lo < hi) {
            if (s[lo] == s[hi]) {
                lo++; hi--;
            } else {
                return validPalindrome(s, lo + 1, hi, count + 1) || 
                        validPalindrome(s, lo, hi - 1, count + 1);
            }
        }
        return true;
    }
};
```


