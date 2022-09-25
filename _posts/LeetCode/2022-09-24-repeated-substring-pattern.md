---
layout: post
title: "Repeated Substring Pattern Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, String Matching ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 459. Given a string s, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

---

<br />

## Description

LeetCode Problem 459.

Given a string s, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

Example 1:
```
Input: s = "abab"
Output: true
Explanation: It is the substring "ab" twice.
```

Example 2:
```
Input: s = "aba"
Output: false
```

Example 3:
```
Input: s = "abcabcabcabc"
Output: true
Explanation: It is the substring "abc" four times or the substring "abcabc" twice.
```

Constraints:
* 1 <= s.length <= 10^4
* s consists of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool repeatedSubstringPattern(string str) {
        string nextStr = str;
        int len = str.length();
        if (len < 1) return false;
        for (int i = 1; i <= len / 2; i++) {
            if (len % i == 0) {
                nextStr = leftShift(str, i);
                if (nextStr == str) return true;
            }
        }
        return false;
    }
    
    string leftShift(string &str, int l) {
        string ret = str.substr(l);
        ret += str.substr(0, l);
        return ret;
    }
};
```


